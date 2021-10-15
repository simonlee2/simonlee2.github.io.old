---
title: "Guide to WWDC19"
date: 2019-06-17T17:09:53+08:00
template: "post"
draft: false
category: "WWDC"
tags:
  - "WWDC"
description: "From SwiftUI, RealityKit, to iPadOS. Find out what's new on the Apple platforms"
---

## Table of Contents
1. [Must watch](#must-watch)
2. [UI](#ui)
3. [AR](#ar)
4. [ML](#ml)
5. [Design](#design)
6. [IAP](#iap)
7. [iPadOS and macOS](#ipad)
8. [Tooling](#tooling)

<a name="must-watch"></a>

## Must Watch
### [Keynote](https://developer.apple.com/videos/play/wwdc2019/101/)  and [Platform State of the Union](https://developer.apple.com/videos/play/wwdc2019/103/)

If you're reading this article, you're probably interested in finding out what happened this year at WWDC. In that case, the Keynote and the Platform State of the Union are the two videos you cannot miss. Keynote is a little more geared towards the consumers and the media, but it sets the tone of the conference. Platform State of the Union is acutally more important for third-party developers like us because it goes into more detail on what app developers should focus on: best practices, changes in frameworks, etc.

### [Introducing SwiftUI: Building Your First App](https://developer.apple.com/videos/play/wwdc2019/204/)

Ask anyone attending WWDC this year about what they're most excited about, and 8 out of 10 will probably say SwiftUI. Rightfully so, SwiftUI is probably one of the biggest paradigm shift since the introduction of Swift and Protocol Oriented Programming.

### [What's New in Swift](https://developer.apple.com/videos/play/wwdc2019/402/)

SwiftUI actually uses a lot of the new features like opaque return type and property wrappers in Swift 5.1 to achieve its new, concise syntax. It's a great session to get familiar with these new features. 

### [Advances in UI Data Sources](https://developer.apple.com/videos/play/wwdc2019/220/)
Many annoucements and improvements this year seem to be overshadowed by SwiftUI, and this introduction on diffable data sources for `UICollectionView` and `UITableViews` is definitely one of the biggest changes coming to UIKit

### [Advances in Collection View Layout](https://developer.apple.com/videos/play/wwdc2019/215/)
Another big change that is under represented among all the annoucements. Learn about "Compositional Layout", a brand new approach in laying out collection views. The new demo app showcases some really complex, yet performant, layouts.

### [Implementing Dark Mode on iOS](https://developer.apple.com/videos/play/wwdc2019/214/)
Dark mode is a thing now and users will expect apps to support them. Learn about everything you need to do in order to support dark mode. 

### [Combine in Practice](https://developer.apple.com/videos/play/wwdc2019/721/)
Combine is an asynchronous event handling framework that looks heavily inspired by React/Rx. Watch this session for a good introduction and code examples.

### [Modernizing Your UI for iOS 13](https://developer.apple.com/videos/play/wwdc2019/224/)
Learn about changes coming to UIKit in iOS 13 – appearances, modal presentations, search bars, gestures, and gestures. 

### [Modern Swift API Design](https://developer.apple.com/videos/play/wwdc2019/415/)
Learn about the latest style on designing APIs for the Apple platforms, with examples from Swift, SwiftUI, and RealityKit

<a name="ui"></a>

## UI

### [Introducing PencilKit](https://developer.apple.com/videos/play/wwdc2019/221/)
We've spent quite some time on doodle-related features (doodle, blur, blemish, cutout). Learn what Apple has done to optimize the performance and what tools are available for us to use in PencilKit.

### [Font Management and Text Scaling](}https://developer.apple.com/videos/play/wwdc2019/227/)
Font management is now an OS feature. Users can use apps to install fonts that will be available system-wide. Learn about the latest on registering and using custom fonts. 

<a name="ar"></a>

## AR
### [Introducing RealityKit and Reality Composer](https://developer.apple.com/videos/play/wwdc2019/603/)
A good introduction on RealityKit, the new 3D rendering engine designer for AR, and RealityComposer, a tool for prototyping and producing content for AR experiences.

### [Introducing ARKit 3](https://developer.apple.com/videos/play/wwdc2019/604/)
The session explores new feature in the third major release of ARKit – including motion capture, people occlusion, multiple face tracking, collaboritve sessions, and a coaching UI. 

### [Bringing People Into AR](https://developer.apple.com/videos/play/wwdc2019/607/)
More technical detail on people occlusion and motion capture

<a name="ml"></a>

## ML
### [What's New in Machine Learning](https://developer.apple.com/videos/play/wwdc2019/209/)
This is the first session to watch if you are interested in machine learning. Get an overview of model personalization, new updates in Vision, Natural Language, Sounds, and Speech. 

### [Understanding Images in Vision Framework](https://developer.apple.com/videos/play/wwdc2019/222/)
A session dedicated to Images in Vision. Learn more about saliency, image classification, similiarity, and face quality.

### [Advances in Camera Capture and Photo Segmentation](https://developer.apple.com/videos/play/wwdc2019/225/)
Learn how to capture photo and videos using mulitple cameras simultaneously. Photo captures now also uses sementic segmentation to provide masks for hair, skin, and teeth.

<a name="design"></a>

## Design
### [Introducing SF Symbols](https://developer.apple.com/videos/play/wwdc2019/206/)
SF symbols is a new set of vector-based symbols that come in various weights and sizes. Learn the benefit of adopting SF symbols as well as how to create new symbols.

### [What's New in iOS Design](https://developer.apple.com/videos/play/wwdc2019/808/)
Learn about the design goals behind dark mode, modal presentations, and contextual menus.

### [Desiging Great ML Experiences](https://developer.apple.com/videos/play/wwdc2019/803/)
Serious technology is hardly usable without a friendly design. Learn how to incorporate ML experiences into your apps, and gain practical approaches to designing user interfaces that feel effortlessly helpful.

### [Designing iPad Apps for Mac](https://developer.apple.com/videos/play/wwdc2019/809/)
Learn about techniques for adapting iPad app's layout for the mac, as well as considerations for text, color, and UI components.

<a name="iap"></a>

## IAP
### [In-App Purchases and Using Server-to-Server Notifications](https://developer.apple.com/videos/play/wwdc2019/302/)
Utilize server-to-server notifications to get the full picture of our subscribers. Use SKStoreFront to get more information about the user's current app store. Learn about the latest updates in StoreKit

<a name="ipad"></a>

## iPadOS and macOS
### [Introducing iPad Apps for Mac](https://developer.apple.com/videos/play/wwdc2019/205/)
Learn how to being rebuilding iPad apps to run natively on the Mac.

### [Introducing Multiple Windows on iPad](https://developer.apple.com/videos/play/wwdc2019/212/)
Introductory session on considerations for adopting multitasking in your app. Whether it makes sense to do it at all and, if it does, what are the steps to create a good mulittasking experience.

<a name="tooling"></a>

## Tooling
### [What's New in Xcode 11](https://developer.apple.com/videos/play/wwdc2019/401/)

Xcode 11 packs plenty of new features and improvements. Some notable additions are source control integrations, Swift Package Manager integration, UI previews, and much more.

### [Creating Great Localized Experiences with Xcode 11](https://developer.apple.com/videos/play/wwdc2019/403/)
The sessions highlights some tools in Xcode that will help streamline the localization workflow. Some of these were new to me, like the xliff, xclocreader, and localization exports.

### [Testing in Xcode](https://developer.apple.com/videos/play/wwdc2019/413/)

Test plans is the new feature for testing in Xcode. Learn how to use test plans to run test against different combination of configurations.

### [What's New in App Store Connect](https://developer.apple.com/videos/play/wwdc2019/301/)
This year Apple introduced a new set of tools and APIs for interacting with App Store Connect. These APIs for managing profiles and certificates may remove the need for third-party API and tools. Learn about updates to Testflight and more.

### [Optimizing Storage in Your App](https://developer.apple.com/videos/play/wwdc2019/419/)
We're looking into app size and storage usage for PicCollage. This session talks about optimization opporunities to reduce the footprint of our apps. 

### [Optimizing App Launch](https://developer.apple.com/videos/play/wwdc2019/423/)
App launch time is also another optimzation we try to continuously improve. Learn how to properly measure launch tie, use instrument to profile app launch, and track launch time over time.
