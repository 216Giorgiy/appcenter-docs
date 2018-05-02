---
title: Managing your Apple ID and certificates | App Center
description: Read how to securely store your Apple ID and iOS signing certificate in App Center.
keywords: Secret storage, Apple ID, certicates
author: oddj0b
ms.author: vigimm 
ms.date: 05/01/2018
ms.topic: article 
ms.assetid: 505ce61e-7647-41cf-8500-459f110944f4
ms.service: vs-appcenter
ms.custom: dashboard
---

# Managing your Apple ID and certificates

## How does Secret storage work
Your Apple ID and certificate are stored securely in an encrypted vault designed so only App Center internal services can read the values. As with any other credentials, you cannot download them after adding to the Secret storage. However, you as the owner can assign them to services in App Center.

## How do I add Apple ID and certificate to storage?
You can add your Apple ID and signing certificate as part of the distribution workflow or from **Account settings** -> **Developer accounts** by clicking the blue + button. Secrets are store in a secure vault, to protect the confidentiality of your credentials.

App Center uses your Apple ID to manage your provisioning profile and your signing certificate to re-sign for a release which includes all testers.

## Planned work
- Enhance secret storage so updates to your credentials are stored across your distribution groups.
- Better support for Apple ID password changes: like certificates, you can add a new password, and continue using the updated Apple ID.
- Information about Apple ID and certificate usage in App Center and a detailed secret overview.

## Feedback
We are continuously improving the experience to improve storing and re-using your Apple developer account secret and are always looking for feedback. If you find errors or shortcomings, please use the blue chat icon in the lower-right corner of the App Center portal to provide your feedback.

