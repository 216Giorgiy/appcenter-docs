---
title: Azure Authentication
description: Authentication methods for Azure and Mobile Center
keywords: azure
author: adrianhall
ms.author: adrianhall
ms.date: 01/20/17
ms.topic: article
ms.assetid: 8d36a5ed-e875-41cc-bd99-f8151705ffcb
ms.service: mobile-center
---

# Identity

Azure Identity enables user authentication for your app without changes to the app backend. It helps protect your application and work with per-user data seamlessly. It is powered by [Azure App Service Authentication / Authorization].

The feature support the following identity providers:
* Azure Active Directory
* Facebook
* Google
* Microsoft Account
* Twitter

You can use multiple providers in a single app, and can choose to utilize client-controlled or server-controlled authentication flow.
* Client flow (recommended): Use an SDK that a given identity provider publishes to establish identity and then gain access to Azure – this allows for better use experience and easier consumption of provider graph APIs.
* Server flow: Use a single line of code from the Azure Identity client SDK to sign in users.


## **Getting Started**

1.  Configure your app with a desired identity provider and establish trust with Mobile Center:
    * [Azure Active Directory]
    * [Facebook]
    * [Google]
    * [Microsoft Account]
    * [Twitter]
2.  Configure your app client to see Identity at work!
    * [iOS][iOS] (Swift or Obj-C)
    * [Android]

[Azure App Service Authentication / Authorization]: https://azure.microsoft.com/en-us/documentation/articles/app-service-authentication-overview/
[Azure Active Directory]: azuread.md
[Facebook]: facebook.md
[Google]: google.md
[Microsoft Account]: microsoft.md
[Twitter]: twitter.md
[iOS]: ~/sdk/azure/identity/ios.md
[Android]: ~/sdk/azure/identity/android.md
