---
title: Configure a Java Android build in Mobile Center
description: How to set up a build system for Android apps
keywords: android
author: siminapasat
ms.author: siminap
ms.date: 01/20/2017
ms.topic: article
ms.assetid: 7042d0ef-50b5-4fdc-bead-bedc9e94923c
ms.service: mobile-center
ms.custom: build
ms.tgt_pltfrm: android
---

# Building Java apps for Android

To start building an app, you will firstly need to connect to your GitHub account, select a repository and a branch where your app lives and then you can set up your first build. Choose the Android project that you would like to build; for the app to run on a real device, the build needs to be code signed with a valid certificate.

## 1. Linking your repository
If you haven't previously connected to your GitHub account, you will firstly need to do that. Once your GitHub account is connected, select the repository where your Android project is located. In order to setup a build for a repository, you need admin and pull rights for it.

## 2. Selecting a branch
Next step once you have selected a GitHub repository is to select the branch you want to build. By default all the active branches will be listed. Upon selecting the branch you want to get started with, it is time to setup your first build!

## 3. Configuring Your Build

To kick off the first build, configure how the Android project should get built:

### 3.1. Build triggers

By default a new build is triggered on every push a developer does to the configured branch. This is often referred to as “Continuous Integration”. If you prefer to manually trigger a new build, you can change this setting in the configuration pane.

### 3.2. Build variant

The available build variants will populate from the Build Types and Product Flavors specified in the build.gradle file. Select which build variant should be built.

### 3.3. Code signing

 A successful build will produce an APK file. In order to release the build to the Play Store, it needs to be signed with a valid certificate stored in a keystore. To sign the builds produced from a branch, enable code signing in the configuration pane, upload your keystore to your repository, and provide the relevant values in the configuration pane. You can read more about code signing [here](~/build/android/code-signing/setup.md).

### 3.4. build.gradle File

Specific information about your build will be collected from your gradle file including dependancies, build tools version, build types, and product flavors.

### 3.5. Distribution to a distribution group

You can configure each successful build from a branch to be distributed to a previously created distribution group. You can add a new distribution group from within the Distribute section. There is always a default distribution group called "Collaborators" that includes all the users who have access to the app.

Once you save the configuration, a new build will be automatically kicked off.

## 4. Build results

After a build has been triggered, it can be in the following states:

* **queued** -  the build is in a queue waiting for resources to be freed up
* **succeeded** - the build is completed and it has succeeded
* **failed** - the build has completed but it has failed; you can troubleshoot what went wrong by downloading and inspecting the build log
* **canceled** - the build has been canceled by a user action or it has timed out

### 4.1. Build logs

For a completed build (succeeded or failed), download the logs to understand more about how the build went. Mobile Center povides an archive with the following files:

```
|-- 1_build.txt (this is the general build log)
|-- build (this folder contains a separate log file for each build step)
    |-- <build-step-1>
    |-- <build-step-2>
    |--
    |-- <build-step-n> (e.g. n_Post Job Cleanup.txt)
```

The build step specific logs (located in the build/ directory of the archive) are helpful for troubleshooting and understanding in what step and why the build failed.

### 4.2. The app package (APK)

The APK is an Android application packaged file which contains the Android app and assets. If the build has been correctly signed, the .apk can be installed on a real device and deployed to the Play Store. If the build has not been signed, the APK can be run on an emulator or used for other purposes.

### 4.3. Building multiple APKs

If your app configuration is set up to build multiple APKs, e.g. different ones per CPU architecture or screen configuration, you need to make sure a universal APK is built as well. Our build system works with one main APK file and will ignore all APKs specific to a certain CPU ABI or screen density. To learn more about APK splits and how to build a universal APK, please read the corresponding [Android developer guide](https://developer.android.com/studio/build/configure-apk-splits.html#configure-abi-split).

## 5. Supported versions and requirements

The minimum version supported to build Android apps is 4.0.3 (API level 15). Android apps can have a lower minimum API level required to run, but have to target at least API level 15.

Apps need to be built with Gradle and the Android Gradle plugin to be configured correctly. Your repository needs to include a Gradle wrapper.
