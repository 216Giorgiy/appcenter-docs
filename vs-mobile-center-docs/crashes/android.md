---
title: Mobile Center Crash Reporting for Android
description: Reporting crashes from Android apps in Mobile Center
keywords: crash reporting
author: BretJohnson
ms.author: BretJohnson
ms.date: 01/20/2017
ms.topic: article
ms.assetid: 38624f1c-15fe-4c9f-8b64-e22348e2dcbc
ms.service: mobile-center
ms.custom: crashes
ms.tgt_pltfrm: android
---

# Android Crashes

> [!div class="op_single_selector"]
- [iOS](ios.md)
- [Android](android.md)
- [React Native](react-native.md)

## Getting Started

1. Integrate the SDK as described in the [Getting Started with Android](~/sdk/android/getting-started/) documentation.
2. Add a test crash to the apps code by calling the `Crashes.generateTestCrash()` method of the crash reporting module as an action to a buttone
3. Run the app without the debugger connected, crash it and restart it
4. After a few minutes the crash report should be visible in the UI

## Troubleshooting

1. *Why are crash reports not visible after a few minutes?*

    Make sure the app doesn't crash on startup, as the SDK wouldn't have time to send the crash report. This is a limitation for any 3rd party crash reporting service which is not possible to overcome.

2. *How can I see de-obfuscated stack traces?*

    This is currently not supported but on our roadmap.

3. *Do you have an Android NDK?*

    This is currently not available but on our roadmap.
