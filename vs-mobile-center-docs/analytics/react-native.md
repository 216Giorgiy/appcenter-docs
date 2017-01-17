---
title: React Native Analytics
description: Analytics for React Native apps
keywords: react native
author: ljzhong
---

# React Native Analytics


This page gives a summary of how to integrate the SDK for Analytics. Should you need more details, the detailed integration instruction can be found at [in the SDK section](~/sdk/getting-started/react-native/).
The SDK section also contains instruction for using CocoaPods

## 1. Add the SDK to the project

In a terminal window opened at the root of your React Native project, enter the following lines to add the Crash service to your app:

```
npm install mobile-center-analytics --save
```

## 2. Link the SDK

Link the plugin to your app with the following command.

```
react-native link mobile-center-analytics
```

You will be asked for your app secrets for Android and iOS, and then asked the following question:

```
For the [platform] app, should user tracking be enabled automatically ? (Use arrow keys)
❯ Enable Automatically
  Enable in JavaScript
```

We recommend you enable automatic event tracking. To understand enabling in JavaScript, [read more here](/sdk/React-Native/analytics/#enable-javascript).

## 3. Analyse

Now build and launch your app, then go to the Analytics section.  You should see 1 Active user and at least 1 session!


## Troubleshooting

### 1. Why are events not appearing in Mobile Center?
  Events passed to Mobile Center must have a name of type `String`. Moreover, the map of `key`:`value` pairs being passed to Mobile Center must be of type `String`:`String`. Passing objects and arrays will cause the method to fail.
