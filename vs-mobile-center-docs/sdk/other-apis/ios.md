---
title: Other iOS APIs
description: Other APIs in the Mobile Center SDK for iOS
keywords: sdk
author: troublemakerben
ms.author: bereimol
ms.date: 04/14/2017
ms.topic: article
ms.assetid: f79abed4-6e50-4d1c-aa1e-0b78b764908d
ms.service: mobile-center
ms.custom: sdk
ms.tgt_pltfrm: ios
dev_langs:  
 - swift
 - objc 
---

# Other iOS APIs

> [!div class="op_single_selector"]
> * [Android](android.md)
> * [iOS](ios.md)
> * [React Native](react-native.md)
> * [UWP](uwp.md)
> * [Xamarin](xamarin.md)

## Adjust the log level

You can control the amount of log messages that show up from Mobile Center in the console. Use the `setLogLevel:`-API to enable additional logging while debugging. By default, it is set to `MSLogLevelAssert` for the App Store environment and `MSLogLevelWarning` otherwise.

To have as many log messages as possible, use `MSLogLevelVerbose`/`MSLogLevel.Verbose`.

```objc
[MSMobileCenter setLogLevel:MSLogLevelVerbose];
```
```swift
MSMobileCenter.setLogLevel(MSLogLevel.Verbose)
```

## Identify installations

The Mobile Center SDK creates a UUID for each device once the app is installed. This identifier remains the same for a device when the app is updated and a new one is generated only when the app is re-installed. The following API is useful for debugging purposes.

```objc
NSUUID *installId = [MSMobileCenter  installId];
```
```swift
var installId = MSMobileCenter.installId()
```

## Disable all services at runtime

If you want to disable all Mobile Center services at once, use the `setEnabled` API. When disabled, the SDK will not forward any information to Mobile Center.

```objc
[MSMobileCenter setEnabled:NO];
```
```swift
MSMobileCenter.setEnabled(false)
```

To enable all services at once again, use the same API but pass `YES`/`true` as a parameter.

```objc
[MSMobileCenter setEnabled:YES];
```
```swift
MSMobileCenter.setEnabled(true)
```

## Use custom properties

The Mobile Center SDK allows you to define custom properties in your app. They are key value pairs. You may use custom properties for various purposes. For instance, you can use custom properties to segment your user, and then send push notifications to a specific [audience](~/push/index.md#audiences).

You can set custom properties by calling the `setCustomProperties` API. A valid key of custom property should match regular expression pattern `^[a-zA-Z][a-zA-Z0-9]*$`. A custom property's value may be one of the following datatypes: `NSString`, `NSNumber`, `BOOL` and `NSDate`.

```objc
[MobileCenter setCustomProperties: [[[MSCustomProperties new] setString:@"blue" forKey:@"color"] setNumber:10 forKey:@"score"]]
```
```swift
MobileCenter.setCustomProperties(MSCustomProperties().setString("blue", forKey: "color").setNumber((10), forKey: "score"))
```
> [!NOTE]
> If you set the same custom property more than once, previous values will be overwritten by the last one.

You may remove any custom property by calling the `clearPropertyForKey` API.

```objc
[MobileCenter setCustomProperties: [[[MSCustomProperties new] setString:@"blue" forKey:@"color"] setNumber:10 forKey:@"score" clearPropertyForKey:@"score"]]
```
```swift
MobileCenter.setCustomProperties(MSCustomProperties().setString("blue", forKey: "color").setNumber((10), forKey: "score").clearProperty(forKey: "score"))
```