---
# required metadata

title: Mobile Center Push for Xamarin.iOS Apps
description: Integrating Mobile Center Push into Xamarin.iOS applications
keywords: sdk, push
author: achocron
ms.date: 05/10/2017
ms.topic: article
ms.assetid: 1fe3506e-ba5c-406d-8ba2-b38a2d1ca588
ms.service: mobile-center
ms.custom: sdk
ms.tgt_pltfrm: xamarin.ios
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

## 1. Enable Apple Push Notifications service (APNS) for your app

For Mobile Center Push to work for an iOS application, you must set up your application to register with Apple's push notification service (APNS). Instructions on how to do this can be found in [Xamarin's documentation](https://developer.xamarin.com/guides/ios/application_fundamentals/notifications/remote_notifications_in_ios/).


## 2. Add Mobile Center Push to your app

Please follow the [Get started](~/sdk/getting-started/uwp.md) section if you haven't set up and started the SDK in your application.

### 2.1. Add the Mobile Center Push package

The Mobile Center SDK is designed with a modular approach – a developer only needs to integrate the modules of the services that they're interested in. It can be integrated using Visual Studio or Package Manager Console.

[!include[](add-nuget.md)]

Now that you've integrated Mobile Center Push in your application, it's time to start the SDK and make use of Mobile Center.

### 2.2. Start Mobile Center Push service

[!include[](start-push.md)]

>[!NOTE]
>If your Xamarin.iOS project is part of a [Xamarin.Forms](xamarin-forms.md) application, it is not necessary to add the call to `MobileCenter.Start()` in the Xamarin.iOS portion of the project. The method call can instead be made from the PCL or shared project portion of your Xamarin.Forms application.

## 4. Enable or disable Push at runtime

[!include[](enable-or-disable.md)]

## 5. Intercept push notifications

[!include[](push-callbacks.md)]
