---
title: Sending Push Notifications
description: Instructions on how to send push notifications using the App Center portal.
keywords: app center, push
author: jwargo
ms.author: jowargo
ms.date: 12/21/2018
ms.topic: article
ms.assetid: 4db077ee-b9bf-4dc7-ac21-e8ecc8ee840e
ms.service: vs-appcenter
ms.custom: push
---

# Sending Push Notifications

The Visual Studio App Center Push service (ACPs) offers two ways to send notifications to registered devices:

+ Using the App Center Portal (described in this document)
+ Using the [App Center Push API](~/push/rest-api.md)

## Creating a notification

To create a notification using the ACPs, complete the following steps:

1. Log into [App Center](https://appcenter.ms).
2. Using the project navigator on the left side of the page, select the your user account or the organization where the app project is defined, then select the app project from the list that appears.
3. In the project navigator that opens, select **Push**.
4. If you've already configured the ACPs, then App Center opens the app project's Push **Notifications** section and lists the existing **Campaigns** for the selected app. If App Center opens the Push getting started page, then you've not configured the service; complete the App Center Push configuration as described in [Configuring the Push Service](~/push/service-config.md) before returning here.
5. In the upper-right corner of the page, click the **Send notification** button.

At this point, App Center opens the **Send notification** wizard and walks you through the process of creating a campaign and sending the notification. The process consists of the following steps:

1. **Compose**: Define your internal name for the campaign, the title and content for the message, and any custom data (key/value pairs) you want included with the message.
2. **Target**: Specify the target audience for the campaign.
3. **Review**: Review the campaign settings one last time.
4. **Send**: Send the notification to the target audience.

The following sections describe each step in the process in greater detail.

### Compose

The first step in the process is to define the internal name for the campaign, and the content that's sent to target devices by App Center.

![App Center Push Campaign Compose page](~/push/images/campaign-compose.png)

//TODO: update the content to describe how the title's used.
//TODO: update the content to list the maximum length allowed for the message

1. Populate the **Campaign Name** field with a descriptive name for the campaign. The value you provide will display in the App Center campaign list page.
2. (optional) Populate the **Title** field with an optional title for the notification sent to target devices. The value you provide here will be #####
3. Populate the **Message** field with the content for the notification message. Message content is limited to ### characters.
4. Use the **Custom data** area of the form to define up to 20 key/value data pairs that you want included with the message. Click the **+** button to add a key/value pair. Click the **-** button to remove a key/value pair from the message.

> [!TIP]
> Custom data values enable campaigns to pass data into an application or trigger one or more actions within your client application. You can pass data directly to the app through a campaign, or send a URL the app uses to retrieve data. Applications can also use data values to set configuration options with in the application, changing app behavior through the campaign. For an implementation example, refer to [A/B Test All the Things: React Native Experiments with App Center](https://blogs.msdn.microsoft.com/vsappcenter/ab-test-all-the-things-react-native-experiments-with-app-center/).

When you're done populating the form, click the **Next >** button to continue.

### Target

When sending notifications through ACPs, you can target destination devices (notification recipients) in the following ways:

+ **All registered devices**: Sends notifications to all registered devices.
+ **Custom devices list**: Sends notifications to up to 20 devices (using the install IDs for the target devices).
+ **Audiences**: Sends notifications to a segment of your app's registered device audience based on a set of device and custom properties.

In the wizard's **Target** panel, make the selection that makes the most sense for your campaign.

#### All registered devices


> [!WARNING]
> No limit on how many, but may take some time

#### Custom device list


#### Audiences

Audiences let you segment your user base based on a set of properties and send them targeted notifications.

An example of an audience could be "App Version = 1.0.0" and "Country = Spain".

These properties can be of two types:

**Device Properties:**

    - App Version
    - Country
    - Mobile Carrier
    - Language
    - Device Model
    - OEM (Original Equipment Manufacturer)
    - API Level
    - Screen Size

**Custom Properties:**

These properties are custom key-value pairs defined by the developer. This will allow you to segment your user based on properties of your app specific.
Examples of custom properties are:

| Key            | Value   |
| -------------- | ------- |
| Type           | Premium |
| Favorite Sport | Premium |

App Center allows you to define custom properties as key value pairs in your app using the App Center SDK. You can then choose this property when you're creating an audience.

You can set these custom properties by using our SDK methods for each platform:

- [Android](~/sdk/other-apis/android.md#use-custom-properties)
- [iOS](~/sdk/other-apis/ios.md#use-custom-properties)
- [UWP](~/sdk/other-apis/uwp.md#use-custom-properties)
- [Xamarin](~/sdk/other-apis/xamarin.md#use-custom-properties)
- [React Native](~/sdk/other-apis/react-native.md#use-custom-properties)
- [macOS](~/sdk/other-apis/macos.md#use-custom-properties)

## Create Audiences

From the audiences tab, select the necessary conditions to create your segment (both custom and device properties), and save your segment. You can later on use this segment when sending a notification.
Another way to create an audience, is when selecting the Audience as a target in the send notification flow.

> [!NOTE]
> Only devices that have Push successfully registered are matched in audiences.

**Limitations**

- The maximum number of Audiences for any App Center app project is 200.
- The default setting for new App Center accounts and accounts with **Basic campaigns** enabled in their billing plan allows for a maximum of 5 audiences per application project. To create more than 5 audiences (up to the maximum of 200), select the "Advanced" option in your billing plan's Push settings. Refer to [App Center Billing](~/general/billing.md) for information on how to change your App Center billing plan.
- App Center limits Audiences to a maximum of 1,000 devices regardless of your billing plan. If you create an audience targeting more than 1,000 devices, App Center Push sends notifications to the first 1,000 devices that match the audience criteria, and skip all remaining devices (failing silently).
- You can define a maximum of 60 custom properties per app project.
- Audiences match only devices that have a valid push registrations. For that reason, testing Audiences on an iOS simulator will fail.


### Review and send the message

In the wizard's last pane, App Center summarizes the settings for the Campaign. To send the notification, click the **Send notification** button. To change the campaign before committing, click the **< Back** button.

![App Center Push Campaign Review page](~/push/images/campaign-review.png)

App Center returns to the Campaigns list; select (click on) the campaign to check delivery progress.