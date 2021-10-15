---
title: "How I learned Docker and deployed a Node.js server"
date: 2017-04-28T23:09:34+08:00
template: "post"
draft: false
category: "Web"
description: "It all started when I asked a friend for help on a project two weeks ago. Having to set up the dev environment for every new machine is tedious and could cause issues down the road. Since I’ve been meaning to learn to use Docker, I decided to dockerize the app, which is a Node.js server and a PostgreSQL database with PostGIS extension that will serve an API for an iOS app."
---

![](https://cdn-images-1.medium.com/max/1600/1*LHzc8Srf5_XBeKzNWdVnfQ.png)

It all started when I asked a friend for help on a project two weeks ago. Having to set up the dev environment for every new machine is tedious and could cause issues down the road. Since I’ve been meaning to learn to use Docker, I decided to dockerize the app, which is a Node.js server and a PostgreSQL database with PostGIS extension that will serve an API for an iOS app.

# Let the journey begin

## Learn the Basics

[The official Docker documentation](https://docs.docker.com/) does a great job walking through the installation of the Docker Engine as well as explaining concepts like containers and services. I won’t repeat them here, but definitely read through the guide if you’re not familiar with Docker.

## Look from Examples

After having a basic understanding of the concepts and tools, I looked for tutorials and projects that have a similar set up as mine. I searched for terms like “docker node postgis”, “docker node postgres”, and “docker server database” to find configurations where containers are separated by roles (app, db, etc). Most projects followed the official Docker documentation and used `docker-compose` to define the interaction among the containers.

Node.js containers usually have a Dockerfile that bundles the app on top of the official Node.js image so that the app will start when the Docker Engine starts a container off of the image.
Database containers are usually simple enough that the configuration is defined directly in the `docker-compose.yml` without its own `Dockerfile`. You can specify an image for the database (`postgres`, `mysql`, `mariadb`, etc), set up environment variables to configure the database, define ports and volumes for the data, and you’ll have a database container up and running.
To sum it up, each container could be an image from Docker Hub or a custom image defined by a `Dockerfile`. A `docker-compose.yml` for the project will orchestrate all the containers involved in the project.

## Dockerize the Node.js server
The server can be dockerized fairly easily. The `Dockerfile` below copies the source code and runs `npm install` on the official Node.js image. The server can be run in a container with a simple `docker build -t server .` and `docker run -p 3000:3000 server npm start`.

```
# Dockerfile
FROM node:7.8.0
# install packages
RUN mkdir -p /usr/src/app
WORKDIR /usr/src
COPY package.json /usr/src
RUN npm install
COPY . /usr/src
EXPOSE 3000
```

## Dockerize the database
I used the `mdillon/postgis` image for PostgreSQL+PostGIS from Docker Hub at first to see if I can get the server and database up and talking to each other.

Here’s what the `docker-compose.yml` looked like at this point:

```
# docker-compose.yml
version: '2'
services:
    db:
        image: mdillon/postgis
        ports:
            - "5432:5432"
        environment:
            - POSTGRES_USER=user
            - POSTGRES_PASSWORD=password
            - POSTGRES_DB=db
    server:
        build: server
        depends_on:
            - db
        ports:
            - "3000:3000"
        command: ["npm", "start"]
```

Here I define a database service using a custom image that creates a PostgreSQL container with PostGIS extensions installed. The server service is built from the `Dockerfile` in the `server` directory. It is declares the database service as a dependency, so `docker-compose` will launch the `db` container before the `service` container.

One caveat of the `depends_on` key is that while the dependencies will be launched first, they may not be ready by the time the server is up. In this particular case, the database service runs a series of scripts to initialize the database and install the PostGIS extensions. During the initialization, the node server may already be up and accepting connections, but the server would not be able to connect to the database.

Docker has [a page addressing the issue and possible solutions](https://docs.docker.com/compose/startup-order/). In the interest of time, I used the [wait-for-it](https://github.com/vishnubob/wait-for-it) script that waits and checks of a TCP host/port is available. I modified the command for server to:

```
command: ["./wait-for-it.sh", "db:5432", "--", "npm", "start"]
```

Now when I run `docker-compose up -d`, the server service will wait and start the server only when the database is ready to accept connections.

## Initialize Database
With the database and server set up, all that’s left is putting some data into the database to let the server do its job. Before dockerizing the app, I had two Node.js scripts for the task: one that creates the tables according to defined schemas and another one populates the database.

Specifically, the the second script fetches data from a third party API, writes it out to the filesystem as a csv file, and runs `COPY` from postgres by reading the csv file. It worked well when the database and the server ran in the same environment, but wouldn’t work when the script and the database run in different containers.

**Solution #1**

My first idea was to handle initialization in the database container, meaning the migration and the copy scripts now have to be run there instead of the server. Unfortunately, that meant that the database container would need not only PostgreSQL and PostGIS but also Node.js. I was able to find a [`Dockerfile`](https://hub.docker.com/r/bryanburgers/node-postgres-postgis/~/dockerfile/) that uses parts from the official PostgreSQL image as well as the [PostGIS image from Appropriate](https://github.com/appropriate/docker-postgis), but the resulting image size grew to just over 1GB.

On top of the large image size, the database container now shares some of the code used to connect to the database from the server as well as dependencies like [knex](http://knexjs.org/) and [knex-postgis](https://github.com/jfgodoy/knex-postgis). I decided it would be a good idea to explore a different approach.

**Solution #2**

Instead of running the initialization in the database container just to have the script and the database in the same environment, I can create a shared volume between the two containers. The script would run on the server container, write csv file to the shared volume, and the database could read the file in the database container using the same shared volume.

```
# docker-compose.yml
version: '2'
services:
    db:
        image: mdillon/postgis
        ports:
            - "5432:5432"
        environment:
            - POSTGRES_USER=user
            - POSTGRES_PASSWORD=password
            - POSTGRES_DB=db
        volumes:
          - data:/usr/src/data
server:
        build: server
        depends_on:
            - db
        volumes:
            - data:/usr/src/data
        ports:
            - "3000:3000"
        command: ["./wait-for-it.sh", "-t", "60`", "db:5432", "--", "npm", "start"]
volumes:
    data: {}
```

With a couple extra lines added to `docker-compose.yml`, we can easily bring up and tear down our dev environment with just a couple commands.

```
# Bring up the containers in the background
docker-compose up -d
# Run the two scripts that initializes the database
docker-compose run --rm server node migrate.js
docker-compose run --rm server node populate.js
# Remove all containers and volumes
docker-compose down
```

## Deployment
It was easy to deploy to DigitalOcean, but it seems like there are two ways to do so:

1. `docker-machine` uses your API token from DigitalOcean to provision remote Docker hosts.
2. `docker-cloud` manages the DigitalOcean droplets through Docker Cloud
I went with `docker-machine` and honestly the set up seems fairly straight forward. Docker has an [excellent guide](https://docs.docker.com/machine/examples/ocean/) that helped me deploy in less than half an hour.

Challenges
Finding relevant resources outside of the official documentation was one of the biggest challenges when I was learning to use Docker. Docker has gone through many releases and best practices change as features are introduced or deprecated. However, this seems to be a common theme in web development as new technologies and frameworks come and go so rapidly.

It might not be a bad idea to change my default date range for search:

`https://www.google.com/search?tbs=qdr:y&q={query}`

## Further Improvements

With the current setup, I feel comfortable enough to move on and start working on the iOS client for this project. However, there are a couple thing I’d like to address down the road:

1. Move database environment variables to a `.env` file. I had tried this at one point but it wasn’t starting the database properly.
2. Is there a better way to initiate the database? Perhaps one that doesn’t involve a shared volume or manually running two scripts to populate the database?
3. Set up continuous integration

> The article is originally posted on [Medium](https://medium.com/@simon_lee/how-i-learned-docker-and-deployed-a-node-js-server-200e742259e5)