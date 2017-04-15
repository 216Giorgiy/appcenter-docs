---
title: Mobile Center Crashes
description:  Mobile Center Crashes for Android
keywords: sdk, crash
author: troublemakerben
ms.author: bereimol
ms.date: 04/14/2017
ms.topic: article
ms.assetid: a9ac95b3-488f-40c5-ad11-99d8da0fa00b
ms.service: mobile-center
ms.custom: sdk
ms.tgt_pltfrm: android
---

1. [Generate a test crash](#1-generate-a-test-crash)
2. [Get more information about a previous crash](#2-get-more-information-about-a-previous-crash)
3. [Enable or disable Mobile Center Crashes at runtime](#3-enable-or-disable-mobile-center-crashes-at-runtime)
4. [Check if Mobile Center Crashes is enabled](#4-check-if-mobile-center-crashes-is-enabled)
5. [Customize your usage of Mobile Center Crashes](#5-customize-your-usage-of-mobile-center-crashes)

# Mobile Center Crashes

> [!div class="op_single_selector"]
> * [Android](android.md)
> * [iOS](ios.md)
> * [React Native](react-native.md)
> * [Xamarin](xamarin.md)

Mobile Center Crashes will automatically generate a crash log every time your app crashes. The log is first written to the device's storage and when the user starts the app again, the crash report will be sent to Mobile Center. Collecting crashes works for both beta and live apps, i.e. those submitted to Google Play. Crash logs contain valuable information for you to help fix the crash.

Please follow the [Getting Started](~/sdk/getting-started/android.md) section if you haven't setup and started the SDK in your application yet.

## 1. Generate a test crash

Mobile Center Crashes provides you with an API to generate a test crash for easy testing of the SDK:

```java
Crashes.generateTestCrash();
```

This API can only be used in test/beta apps and won't do anything in production apps.

## 2. Get more information about a previous crash

Mobile Center Crashes has two API that give you more information in case your app has crashed.

### 2.1 Did the app crash in last session?

At any time after starting the SDK, you can check if the app crashed in the previous launch:

```java
Crashes.hasCrashedInLastSession();
```
This comes in handy in case you want to adjust the behavior or UI of your app after a crash has occured. Some developers chose to show additional UI to apologize to their users, or want way to get in touch after a crash has occured. 

### 2.2 Details about the last crash

If your app crashed previously, you can get details about the last crash.

```java
Crashes.getLastSessionCrashReport(new ResultCallback<ErrorReport>() {
 @Override
 public void onResult(ErrorReport data) {
     if (data != null) {
         Log.i("MyApp", "Last session crash details=", data.getThrowable());
     }
  }
});
```

There are numerous use cases for this API, the most common one is people who call this API and implement their custom [CrashesListener](#5-customize-your-usage-of-mobile-center-crashes). 


## 3. Enable or disable Mobile Center Crashes at runtime

You can enable and disable Mobile Center Crashes at runtime. If you disable it, the SDK will not do any crash reporting for the app.

```java
Crashes.setEnabled(false);
```

To enable Mobile Center Crashes again, use the same API but pass `true` as a parameter.

```java
Crashes.setEnabled(true);
```

## 4. Check if Mobile Center Crashes is enabled

You can also check if Mobile Center Crashes is enabled or not:

```java
Crashes.isEnabled();
```

## 5. Customize your usage of Mobile Center Crashes

Mobile Center Crashes provides callbacks for developers to perform additional actions before and when sending crash logs to Mobile Center.

To handle the callbacks, you must either implement all methods in the `CrashesListener` interface, or override the `AbstractCrashesListener` class and pick only the ones you're interested in.

### 5.1 Use your own CrashesListner

Create your own CrashesListener and assign it like this:

```java
CrashesListener customListener = new CrashesListener() {
	// Implement all callbacks here.
};
Crashes.setListener(customListener);
```

In case you are only interested in customizing one of the callbacks, use the `AbstractCrashesListener` instead: 

```java
AbstractCrashesListener customListener = new AbstractCrashesListener() {
	// Implement any callback here as required.
};
Crashes.setListener(customListener);
```

### 5.2 Should the crash be processed?

Implement this callback if you'd like to decide if a particular crash needs to be processed or not. For example, there could be a system level crash that you'd want to ignore and don't want to send to Mobile Center.

```java
boolean CrashesListener.shouldProcess(ErrorReport report) {
     return true; // return true if the crash report should be processed, otherwise false.
}
```

### 5.3 Ask for the user's consent to send a crash log

If user privacy is important to you, you might want to get your users' confirmation before sending a crash report to Mobile Center. The SDK exposes a callback that tells Mobile Center Crashes to await your user's confirmation before sending any crash reports.
If you chose to do so, you are responsible for obtaining the user confirmation, e.g. through a dialog prompt with one of these options - "Always Send", "Send", and "Don't send". Based on the user input, you will tell the Mobile Center Crashes what to do and the crash will then be handled accordingly.

```java
boolean CrashesListener.shouldAwaitUserConfirmation() {
	return true; // Return true if the SDK should await user confirmation, otherwise false.
}
```

If you return `true`, your app must obtain the user's permission and message the SDK with the result using the following API:

```java
Crashes.notifyUserConfirmation(int userConfirmation);
```

Pass one option of `SEND`, `DONT_SEND` or `ALWAYS_SEND` in the above method call.

Feel free to have a look [at our reference implementation](https://github.com/Microsoft/mobile-center-sdk-android/blob/develop/apps/sasquatch/src/main/java/com/microsoft/azure/mobile/sasquatch/activities/MainActivity.java#L104).

### 5.4 Get information about the sending status for a crash log

In our experience, developers might be interested about the status of Mobile Center Crashes. A common use case is that you might want to show UI that tells the users that your app is submitting a crash report, or, in case your app is crashing very quickly after the launch, you want to adjust the behavior of the app to make sure the crash logs can be submitted. Mobile Center Crashes has three different callbacks that you can use in your app to be notified of what is going on:

* Before a crash log is sent, the following callback will be invoked: 

	```java
	void CrashesListener.onBeforeSending(ErrorReport report) {
		// Your code goes here.
	}
	```
	
* After sending a crash log was successful, the callback will be invoked :

	```java
	void CrashesListener.onSendingSucceeded(ErrorReport report) {
		// Your code goes here.
	}
	```
   
* After sending a crash log failed, the following callback will be invoked:

	```java
	void CrashesListener.onSendingFailed(ErrorReport report, Exception e) {
		// Your code goes here.
	}
	```