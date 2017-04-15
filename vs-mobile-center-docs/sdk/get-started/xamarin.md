---
title: Get started
description: Get started
keywords: sdk
author: troublemakerben
ms.author: bereimol
ms.date: 04/14/2017
ms.topic: get-started-article
ms.assetid: 466c0195-c2c7-491b-83dc-2ec03dd9ab18
ms.service: mobile-center
ms.custom: sdk
ms.tgt_pltfrm: xamarin
---

1. [Prerequisites](#1-prerequisites)
2. [Create your app in the Mobile Center Portal](#2-create-your-app-in-the-mobile-center-portal-to-optain-the-app-secret)
2. [Add Mobile Center SDK modules](#3-add-mobile-center-sdk-modules)
3. [Start the SDK](#3-start-the-sdk)

# Get started

> [!div class="op_single_selector"]
> * [iOS](ios.md)
> * [Android](android.md)
> * [React Native](react-native.md)
> * [Xamarin](xamarin.md)

The Mobile Center SDK uses a modular architecture so you can use any or all of the services.

Let's get started with setting up Mobile Center Android SDK in your app to use Mobile Center Analytics and Mobile Center Crashes. To add Mobile Center Distribute to you app, please have a look at the [documentation for Mobile Center Distribute](~/sdk/distribute/xamarin).

## 1. Prerequisites

Before you begin, please make sure that the following prerequisites are met:

* Your project is set up in Xamarin Studio or Xamarin for Visual Studio.
* You are tarketing devices running iOS 8.0 or later or Android 4.0.3 (API level 15) or later
* You are not using any other SDK that provides Crash Reporting functionality.

The Mobile Center SDK for Xamarin supports the following platforms:

* Xamarin.iOS
* Xamarin.Android
* Xamarin.Forms (iOS and Android)

### 1.1 About Xamarin.iOS

Choose this option if you target no other platform but iOS. You need to create one app in the Mobile Center portal with **iOS** as the OS and **Xamarin** as the platform.

### 1.2 About Xamarin.Android
  
Choose this option if you target no other platform but Android. You need to create one app in the Mobile Center portal with the **Android** as the OS and **Xamarin** as the platform.

### 1.3 About Xamarin.Forms (iOS and Android)
 
Choose this option if you want to create a cross platform app for iOS and Android devices. You need to create two apps in Mobile Center – one for each OS – and select **Xamarin** as the platform for each of them.

## 2. Create your app in the Mobile Center Portal to optain the App Secret

If you have already created your app in the Mobile Center portal, you can skip this step.

1. Head over to [mobile.azure.com](https://mobile.azure.com).
2. Sign up or log in and hit the blue button on the top right corner of the portal that says **Add new** and select **Add new app** from the dropdown menu.
2. Enter a name and an optional desciption for you app.
3. Select the appropriate OS and platform depending on your project as described above.
4. Hit the button at the bottom right that says **Add new app**.

Once you have created an app, you can optain it's **App Secret** on the **Getting Started** or **Manage App** sections of the Mobile Center Portal.


## 3. Add the Mobile Center SDK modules

The Mobile Center SDK can be integrated using Xamarin Studio, Xamarin for Visual Studio, or using the Package Manager Console. 

> [!NOTE]
> Due to a bug in Xamarin.iOS 10.4, you also need to *uncheck* **Enable incremental builds** in your iOS project's **Build Options**.

### 3.1 Xamarin Studio

#### 3.1.1 Xamarin.iOS and Xamarin.Android

* Navigate to the **Project -> Add NuGet Packages...**
* Search for **Mobile Center**, and select **Mobile Center Analytics** and **Mobile Center Crashes**. Then Click **Add Packages**.

#### 3.1.2 Xamarin.Forms

Multiplatform Xamarin.Forms apps have three projects in your solution - the portable class library or shared library, the Android project `project.Droid` and the iOS project `project.iOS` . You need to add the NuGet packages to each of these projects.

* Navigate to the **Project -> Add NuGet Packages...**
* Search for **Mobile Center**, and select **Mobile Center Analytics** and **Mobile Center Crashes**. Then Click **Add Packages**.

### 3.2 Xamarin for Visual Studio

* Navigate to the **Project -> Manage NuGet Packages...**
* Search for **Mobile Center**, and select **Mobile Center Analytics** and **Mobile Center Crashes**. Then Click **Add Packages**.

### 3.3 Package Manager Console ##

* Make sure the Package Manager Console is opened in either Xamarin Studio or Visual Studio. You will have to install an add-in for Xamarin Studio.
* Type the following commands:

   `PM> Install-Package Microsoft.Azure.Mobile.Analytics`
   `PM> Install-Package Microsoft.Azure.Mobile.Crashes`


Now that you've integrated the SDK in your application, it's time to start the SDK and make use of the Mobile Center services.


## 4. Start the SDK

In order to use Mobile Center, you need to opt in to the module(s) that you want to use, meaning by default no modules are started and you will have to explicitly call each of them when starting the SDK.

### 4.1 Add the using statements

Add the appropriate namespaces befor eyou get started with using our APIs.

* **Xamarin.iOS** - Open you `AppDelegate.cs` and add the lines below the existing using statements
* **Xamarin.Android** - Open your `MainActivity.cs` and add the lines below the existing using statements
* **Xamarin.Forms** - Open your `App.xaml.cs` in your shared project and add the following using statements
	
```csharp
using Microsoft.Azure.Mobile;
using Microsoft.Azure.Mobile.Analytics;
using Microsoft.Azure.Mobile.Crashes;
```

### 4.2 Add the `start()`-method

**Start the SDK:** Mobile Center provides developers with three modules to get started – Analytics, Crashes and Distribute. In order to use these modules, you need to opt in for the module(s) that you'd like, meaning by default no module is started and you will have to explicitly call each of them when starting the SDK.

#### 4.2.1 Xamarin.iOS

Open your `AppDelegate.cs` and add the `start()`-call inside the `FinishedLaunching()` method

```csharp
MobileCenter.Start("{Your Xamarin iOS App Secret}", typeof(Analytics), typeof(Crashes));
	```

#### 4.2.2 Xamarin.Android

Open `MainActivity.cs` and add the `start()`-call inside the `OnCreate()` method

```csharp
MobileCenter.Start("{Your Xamarin Android App Secret}", typeof(Analytics), typeof(Crashes));
```

##### 4.2.3 Xamarin.Forms

For creating a Xamarin.Forms application targeting both iOS and Android platforms, you need to create two applications in the Mobile Center portal - one for each platform. Creating two apps will give you two App secrets - one for iOS and another one for Android. Open your `App.xaml.cs` (or your class that inherits from `Xamarin.Forms.Application`) in your shared or portable project and add the method below in the `OnStart()` override method.

```csharp
MobileCenter.Start("ios={Your Xamarin iOS App Secret};android={Your Xamarin Android App secret}", typeof(Analytics), typeof(Crashes));
```
	
### 4.3 Replace the placeholder with your App Secret

Make sure to replace `{Your App Secret}` text with the actual value for your application. The App Secret can be found on the **Getting Started** page on the Mobile Center portal or through the **Manage App** button.

The Getting Started page contains the above code sample with your App Secret in it, you can just copy-paste the whole sample.

The example above shows how to use the `start()`-method and include both Mobile Center Analytics and Mobile Center Crashes.

If you do not want to use one of the two services, remove the corresponding parameter from the method call above.

Note that, unless you explicitly specify each module as parameters in the start method, you can't use that Mobile Center service. In addition, the `start()`-API can be used only once in the lifecycle of your app – all other calls will log a warning to the console and only the modules included in the first call will be available.

For example - If you just want to onboard to Mobile Center Analytics, you should modify the `start()`-call call as follows:

```csharp
MobileCenter.Start("{Your Xamarin Android App Secret}", typeof(Analytics));
```

Great, you are all set to visualize Analytics and Crashes data on the portal that the SDK collects automatically.

Look at the documentaton for [Mobile Center Analytics](~/sdk/analytics/xamarin.md) and [Mobile Center Crashes](~/sdk/crashes/xamarin.md) to learn how to customize and use more advanced functionalities of both services.

To learn how to get started with in-app updates, head over to the documentation of [Mobile Center Distribute](~/sdk/distribute/xamarin.md).
