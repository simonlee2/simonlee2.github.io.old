---
title: "Accelerate Your Team with Continuous Delivery"
date: 2019-05-20T15:08:10-07:00
template: "post"
draft: false
slug: "accelerate-your-team-with-continuous-delivery"
category: "Reading"
description: "24 key capabilities that drive improvement in software delivery performance and, in turn, organizational performance..."
---

<!-- ![Accelerate](/accelerate-cover.jpg) -->

In _[Accelerate](https://www.amazon.com/Accelerate-Software-Performing-Technology-Organizations-ebook/dp/B07B9F83WM)_, Nicole Forsgren, Jez Humble, and Gene Kim present the methods and results of their four-year research program. They have identified 24 key capabilities that drive improvement in software delivery performance and, in turn, organizational performance. 

They've classified these capabilities into five categories:

1. Continuous delivery
2. Architecture
3. Product and process
4. Lean management and monitoring
5. Cultural

Today, we will highlight the capabilities that allow us to achieve continuous delivery.

--- 

## Use version control for all production artifacts

Using version control is already a common practice for software teams. Everything that's needed to create a production build (application code, configurations, build scripts, etc.) should be checked in under version control. 

## Use trunk-based development methods

Trunk-based devlopment refers to the practice where the teams keep the number of active branches low and the lifetime of these branches short before merging into master. Adopting trunk-based development allows changes to be integrated with master as early as possible, which enables the team to better achieve continuous integration and continuous delivery. 

## Automate your deployment process

Automate the deployment process as much as possible so that deployment becomes a trivial task. 

## Implement test automation

Developers should implement unit and UI tests that are run automatically throughout the development process. The tests should be reliable in that they should find real failures and only pass releasable code.

## Implememt continuous integration

A proper continous integration should regularly integrate code changes into the main branch and run automated test suites to check for new bugs or regressions that developer can quickly fix.

## Implement continuous delivery

Adopting continuous devliery enables the team to deploy all the latest changes at any time with little manual work. An example of this would be to deploy a build for every change on master, or to release a daily build. The team should try to keep software in a deployable state, and if it becomes undeployable, fixes are made quickly.

## Support test data management

Ensure that there is enough test data to run automated tests and that it is easy to acquire more test data.

## Shift left on security

Move software security earlier in the delivery process so that any issues are avoided or resolved sooner. Integrate security practices into the software delivery lifecycle in a way that does not slow down the developemtn process.

---

## Conclusion

Unlocking these capabilities for your team allows them deploy faster, more frequently, and more reliably, which, according to the research presented in the book, will improve the overall performance of your team. How many of these capabilities has you team implemented? 
