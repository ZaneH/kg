---
title: Mobile Programming
tags: mobile, code
date: 08-26-2023
---
## The Rundown

Mobile programming is the process of creating applications for mobile devices like smartphones and tablets. As mobile web browsers rapidly improved, some developers opt to create their apps as "web apps" instead of building "an app."

One of the main benefits of opting for a web app is that it's more democratized. Apple and Google are the gatekeepers of their respective app stores.

## Native vs Cross-Platform Frameworks

- **Native frameworks** make apps that are specific to a particular mobile operating system. For example, Swift and Objective-C are used for iOS, and Java or Kotlin are used for Android. Native apps tend to perform better and provide a more consistent look-and-feel with the device's operating system, because they have direct access to all of the device's hardware and OS-specific features.

- **Cross-Platform frameworks**, like React Native, allow developers to write code once and deploy it across multiple platforms. This approach is more cost-effective and faster because it enables the reuse of code across different platforms. However, cross-platform apps may have performance drawbacks and inconsistencies in appearance or behavior compared to native frameworks.

## React Native

React Native is a popular cross-platform framework that allows developers to build mobile apps using JavaScript and React JSX syntax. As in React for [[code/overview/frontend-web-development|web development]], React Native enables component-based architecture, which promotes code reuse and improves the codebase's maintainability. 

Here are some key points regarding my experience with React Native:

- It's quite similar to React, meaning that converting a web developer into a mobile developer can be accomplished with relative ease.
- It allows the creation of truly native apps, from one codebase, for both iOS and Android. React Native is also compatible with the web.
- React Native is efficient, as it allows for hot reloading, which keeps the app running while you edit files.

## Expo

Expo is my preferred framework for React Native. It streamlines the process of building and deploying React Native apps. Some of the benefits of using Expo include:

- There's no need for Xcode or Android Studio, which simplifies the setup process.
- It gives developers access to native APIs through an easy-to-use JavaScript interface.
- It provides Over-the-Air updates, meaning that developers can publish updates to their apps without needing the user to update via app stores.

Expo is an excellent tool for beginners in mobile development because of its ease of use. However, for apps that require custom native code, Expo might not be suitable. But for most general use cases, it is a powerful and efficient tool.

## Flutter

Flutter is a modern cross-platform framework developed by Google. It lets you build apps for multiple platforms (iOS, Android, web) from a single codebase, using the Dart programming language. Here's a quick rundown:

**Pros:**
- **Single Codebase:** Write code once, deploy on multiple platforms (including web.)
- **Custom UI:** Create highly customizable and visually appealing interfaces.
- **Performance:** Near-native performance due to direct compilation to native ARM code.
- **Hot Reload:** Instantly see code changes, speeding up development.

**Cons:**
- **Learning Curve:** Dart might require some getting used to. It introduces new patterns I haven't seen outside of Flutter personally.
- **Less Native Feel:** While close, the UI might not feel entirely native on some platforms.
- **Limited Libraries:** Smaller ecosystem compared to more established frameworks.

I think Flutter has a bit more work to do before I use it for anything serious. It is great for implementing complex user interfaces, but there is a cost and it becomes apparent when you start diving into streams, sinks, BLoC, etc.