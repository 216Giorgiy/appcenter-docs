---
# required metadata

title: Mobile Center Push for Xamarin.Android Apps
description: Integrating Mobile Center Push into Xamarin.Android applications
keywords: sdk, push
author: achocron
ms.date: 05/10/2017
ms.topic: article
ms.assetid: 3f3e83cd-0f05-455e-8e67-6b6d5042949d
ms.service: mobile-center
ms.custom: sdk
ms.tgt_pltfrm: xamarin.android
---

# Mobile Center Push

> [!div class="op_single_selector"]
> * [Android](android.md)
> * [iOS](ios.md)
> * [UWP](uwp.md)
> * [Xamarin.Android](xamarin-android.md)
> * [Xamarin.iOS](xamarin-ios.md)
> * [Xamarin.Forms](xamarin-forms.md)

Mobile Center Push enables you to send push notifications to users of your app from the Mobile Center portal.

## 1. Add Firebase to your app

To send push notifications to your applications, Mobile Center integrates with [Firebase Cloud Messaging](https://firebase.google.com/docs/cloud-messaging/).

>[!NOTE]
>Only devices having the [Google Play](https://play.google.com) store application or emulators with *Google APIs* images can receive the notifications.

>[!NOTE]
>Firebase displays a notification in the system notification center only if the application is in the background at the moment the push is received.

### 1.1. Create a Firebase project

The first step in integrating your application with Mobile Center Push is to integrate it with Firebase Cloud Messaging. Start by creating a Firebase project in Google's [Firebase console](https://console.firebase.google.com). Sign in with your Google account and proceed to the console. To create a Firebase project, select the **add project** button. Next, enter a project name and select **Create Project**.

Now that you've created a Firebase project, you must configure your application to receive Firebase notifications. On the side menu, select **Notifications** to navigate to the notifications page. To configure your application to receive notifications, select the Android logo (the button to the right of the one that says "iOS").

![firebase-notifications-page](images/firebase-add-notifications.png)

Follow steps **one** and **two** in the setup window. Since you are creating a Xamarin application, you may ignore step **three**. Finally, make sure to note where you save the *google-services.json* file, as you will need it later.

### 1.2. Obtain your Android API Key
Go to Project Settings and under Cloud Messaging, copy your Server Key. This will be the Android API Key that you will need to include in the Mobile Center Push portal.

### 1.3. Customize Proguard configuration

To ensure that the Proguard optimizer doesn't remove certain classes, you must customize its configuration.

#### 1.3.1. Create a Proguard configuration file

>[!NOTE]
>If you already have a Proguard configuration file in your project, you may skip to step 1.3.2.

Add an empty file to your Xamarin.Android project named *proguard.cfg*. Set the build action to "ProguardConfiguration."

![proguard-configuration-build-action](images/proguard-configuration-build-action.png)

#### 1.3.2. Add customization to Proguard configuration file
In your Xamarin.Android project, please add the following lines to your `proguard.cfg` file:

```
-dontwarn com.google.android.gms.**
-keep class com.google.firebase.provider.FirebaseInitProvider
-keep class com.google.firebase.iid.FirebaseInstanceIdReceiver
-keep class com.microsoft.azure.mobile.push.TokenService
-keep class com.microsoft.azure.mobile.push.PushMessagingService
```

## 2. Add Mobile Center Push to your app

Please follow the [Get started](~/sdk/getting-started/xamarin.md) section if you haven't set up and started the SDK in your application yet.

### 2.1. Add the Mobile Center Push module

[!include[](add-nuget.md)]

### 2.2. Add the google-services.json File
Locate the *google-services.json* file from step 1 and add it to your project. Set the build action to "GoogleServicesJson."

![google-services-json-build-action](images/google-services-json-build-action.png)

> [!IMPORTANT]
> If you do not see this option under build actions, make sure you've added the Mobile Center Push NuGet package already. If you have and it still doesn't appear, try restarting your IDE.

### 2.3. Modify AndroidManifest.xml

Edit **AndroidManifest.xml** and insert the following `<receiver>` elements into the `<application>` section:

```xml
  <receiver 
      android:name="com.google.firebase.iid.FirebaseInstanceIdInternalReceiver" 
      android:exported="false" />
  <receiver 
      android:name="com.google.firebase.iid.FirebaseInstanceIdReceiver" 
      android:exported="true" 
      android:permission="com.google.android.c2dm.permission.SEND">
      <intent-filter>
          <action android:name="com.google.android.c2dm.intent.RECEIVE" />
          <action android:name="com.google.android.c2dm.intent.REGISTRATION" />
          <category android:name="${applicationId}" />
      </intent-filter>
  </receiver>
```

### 2.4. Start Mobile Center Push

[!include[](start-push.md)]

>[!NOTE]
>If your Xamarin.Android project is part of a [Xamarin.Forms](xamarin-forms.md) application, it is not necessary to add the call to `MobileCenter.Start()` in the Xamarin.Android portion of the project. The method call can instead be made from the PCL or shared project portion of your Xamarin.Forms application.

## 3. Existing Firebase Analytics users

Mobile Center Push has a dependency on Firebase.

Firebase Analytics is included in the core Firebase module and is thus a dependency of Firebase messaging.

As a result, our SDK automatically disables Firebase Analytics to prevent unwanted data collection by Firebase.

If you are a customer of Firebase Analytics and want to keep reporting analytics data to Firebase, you need to call `Push.EnableFirebaseAnalytics()` before `MobileCenter.Start()` like so:

```csharp
Push.EnableFirebaseAnalytics();
MobileCenter.Start("{Your App Secret}", typeof(Analytics), typeof(Crashes), typeof(Push));
```

## 4. Enable or disable Push at runtime

[!include[](enable-or-disable.md)]

## 5. Intercept push notification in the foreground

[!include[](push-callbacks.md)]
