---
title: Mobile Center Distribute
description: Using in-app updates in Mobile Center Distribute
keywords: sdk, distribute
author: troublemakerben
ms.author: bereimol
ms.date: 04/14/2017
ms.topic: article
ms.assetid: f91fcd0b-d5e6-4c74-89a8-f71c2ee57556
ms.service: mobile-center
ms.custom: sdk
ms.tgt_pltfrm: ios
---

1. [Add in-app updates to your app](#1-add-in-app=updates-to-your-app)
2. [Customize or localize the in-app update dialog](#2-customize-or-localize-the-in-app-update-dialog)
3. [Enable or disable Mobile Center Distribute at runtime](#3-enable-or-disavle-mobile-center-distribute-at-runtime)
4. [Check if Mobile Center Distribute is enabled](#4-check-if-mobile-center-distribute-is-enabled)
5. [Don't initialise Mobile Center Distribute during development](#5-dont-initialise-mobile-center-distribute-during-development)

# Mobile Center Distribute

> [!div class="op_single_selector"]
> * [Android](android.md)
> * [iOS](ios.md)
> * [Xamarin](xamarin.md)

Mobile Center Distribute will let your users install a new version of the app when you distribute it via the Mobile Center. With a new version of the app available, the SDK will present an update dialog to the users to either download or ignore the new version. Once they chose to update, the SDK will start to update your application. This feature will NOT work if your app is deployed to the app store.

In addition, please have a look at the information on how to [utilize Mobile Center Distribute](~/distribution/index.md) if you haven't done it, yet.
While it is possible to use Mobile Center Distribute to distribute a new version of your app without adding any code, adding Mobile Center Distribute to your app's code will result in a more seamless experience for your testers and users as they get the in-app update experience.

## 1. Add in-app updates to your app

Please follow the [Get started](~/sdk/getting-started/ios.md) section if you haven't setup and started the SDK in your application, yet.

### 1.1 Add the Mobile Center Distribute module

The Mobile Center SDK is designed with a modular approach – a developer only needs to integrate the modules of the services that they're interested in.


#### 1.1.1 Integration using Cocoapods

If you are integrating Mobile Center into your app using Cocoapods, add the following dependency to your podfile and run `pod install`.

```ruby
pod 'MobileCenter/MobileCenterDistribute`
```

#### 1.1.2 Integration by copying the binaries into your project

1. Download the [Mobile Center iOS SDK](https://github.com/Microsoft/MobileCenter-SDK-iOS/releases) frameworks provided as a zip file.

2. Unzip the file and you will see a folder called `MobileCenter-SDK-iOS` that contains different frameworks for each Mobile Center service. The framework called `MobileCenter` is required in the project as it contains code that is shared between the different modules.

3. [Optional] Create a subdirectory for 3rd-party-libraries.
 	* As a best practice, 3rd-party libraries usually reside inside a subdirectory (it is often called `Vendor`), so if you don't have your project organized with a subdirectory for libraries, now would be a great start for it.
 	* Create a group called `Vendor` inside your Xcode project to mimic your file structure on disk.

4. Open Finder and copy the previously unzipped `MobileCenter-SDK-iOS` folder into your project's folder at the location where you want it to reside.

5. Add the SDK framework to the project in Xcode:
    * Make sure the Project Navigator is visible (⌘+1).
    * Now drag and drop `MobileCenter.framework`, `MobileCenterDistribute.framework` and `MobileCenterDistributeResources.bundle` from the Finder (the ones inside the Vendor folder) into your Xcode's Project Navigator. Note that `MobileCenter.framework` is required to start the SDK, make sure it iss added to your project, otherwise the other modules won't work and your app won't compile.
    * A dialog will appear, make sure your app target is checked. Then click **Finish**.


### 1.2 Start Mobile Center Distribute

In order to use Mobile Center, you need to opt in to the module(s) that you want to use, meaning by default no modules are started and you will have to explicitly call each of them when starting the SDK. 

#### 1.2.1 Add the import for Mobile Center Distribute

**Objective-C**

Open your `AppDelegate.m` file and add the following import statements.

```obj-c
@import MobileCenter;
@import MobileCenterDistribute;
```

**Swift**

Open your `AppDelegate.swift` file and add the following import statements.

```swift
import MobileCenter
import MobileCenterDistribute
```

#### 1.2.2 Add the `start:withServices:` method

Add `MSDistribute` to your `start:withServices:` method to start Mobile Center Distribute together with the other services that you want to use in your app.

**Objective-C**

Insert the following line to start the SDK in your app's `AppDelegate.m` class in the `didFinishLaunchingWithOptions` method.

```obj-c
[MSMobileCenter start:@"{Your App Secret}" withServices:@[[MSAnalytics class], [MSCrashes class], [MSDistribute class]]];
```

**Swift**

Insert the following line to start the SDK in your app's `AppDelegate.swift` class in the `didFinishLaunchingWithOptions` method.

```swift
MSMobileCenter.start("{Your App Secret}", withServices: [MSAnalytics.self, MSCrashes.self, MSDistribute.self])
```

Make sure you have replaced `{Your App Secret}` in the code sample above with your app's App Secret. Please also check out the [Get started](~/sdk/getting-started/ios.md) section if you haven't setup and started the SDK in your application, yet.

#### 1.3 Modify your `info.plist`

1. Open your `Info.plist`.
2. Add a new key for `URL types` or `CFBundleURLTypes` (in case Xcode displays your `Info.plist` as source code).
3. Change the key of the first child item to URL Schemes or `CFBundleURLSchemes`.
4. Enter `mobilecenter-${APP_SECRET}` as the URL scheme and replace `${APP_SECRET}` with the App Secret of your app.

#### 1.4 Implement the `openURL:`-callback

Implement the `openURL`-callback in your `AppDelegate` to enable in-app-updates.

**Objective-C**

```obj-c
- (BOOL)application:(UIApplication *)application
	            openURL:(NSURL *)url
	  sourceApplication:(NSString *)sourceApplication
	         annotation:(id)annotation {
	         
	// Pass the url to MSDistribute.
	[MSDistribute openUrl:url];
	return YES;
}
```

**Swift**

```swift
func application(_ application: UIApplication, open url: URL, sourceApplication: String?, annotation: Any) -> Bool {
	    
  // Pass the URL to MSDistribute.
  MSDistribute.open(url as URL!)
  return true
}
```

## 2. Customize or localize the in-app update dialog

You can easily provide your own resource strings if you'd like to localize the text displayed in the update dialog. Look at the string files [this resource file](https://github.com/Microsoft/mobile-center-sdk-ios/blob/develop/MobileCenterDistribute/MobileCenterDistribute/Resources/en.lproj/MobileCenterDistribute.strings). Use the same string name and specify the localized value to be reflected in the dialog in your own app resource files.   

## 3. Enable or disable Mobile Center Distribute at runtime

You can enable and disable Mobile Center Distribute at runtime. If you disable it, the SDK will not provide any in-app update functionality.

> [!NOTE]
> Note that it will only disable SDK features for the Distribute service (in-app updates for your application) and the SDK API has nothing to do with disabling the Distribute service on the Mobile Center portal.

**Objective-C**

```objectivec
[MSDistribute setEnabled:NO];
```

**Swift**

```swift
MSDistribute.setEnabled(false)
```

To enable Mobile Center Distribute again, use the same API but pass `YES`/`true` as a parameter.

```objectivec
[MSDistribute setEnabled:YES];
```

**Swift**

```swift
MSDistribute.setEnabled(true)
```

## 4. Check if Mobile Center Distribute is enabled

You can also check if Mobile Center Distribute is enabled or not:

**Objective-C**

```objectivec
BOOL enabled = [MSDistribute isEnabled];
```

**Swift**

```swift
var enabled = MSDistribute.isEnabled()
```

##  5. Don't initialise Mobile Center Distribute during development
 
Mobile Center Distribute will pop up it's UI/browser at application start. While this is an expected behavior for your end users it could be disruptive for you during the development stage of your application. We recommend to not initialize `MSDistribute` for your `DEBUG` configuration.

 **Objective-C**
 
 ```objectivec
 #if DEBUG
 	[MSMobileCenter start:@"YOUR_APP_ID" withServices:@[[MSAnalytics class], [MSCrashes class]]];
 #else
 	[MSMobileCenter start:@"YOUR_APP_ID" withServices:@[[MSAnalytics class], [MSCrashes class], [MSDistribute class]]];
 #endif
 ```
 
 **Swift**
 
 ```swift
 #if DEBUG
 	MSMobileCenter.start("YOUR_APP_ID", withServices: [MSAnalytics.self, MSCrashes.self])
 #else
 	MSMobileCenter.start("YOUR_APP_ID", withServices: [MSAnalytics.self, MSCrashes.self, MSDistribute.self])
 #endif
 ``` 