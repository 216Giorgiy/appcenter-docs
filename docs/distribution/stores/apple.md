---
title: Publish to iTunes
description: Simplify distribution of mobile applications to the App Store
keywords: distribution store
author: oddj0b
ms.author: vigimm
ms.date: 08/23/2018
ms.topic: article
ms.service: vs-appcenter
ms.custom: distribute
---

# App Store and TestFlight Distribution 

Publish iOS app upgrades to the App Store and TestFlight.

## Pre-requisites

* The first version of an iOS application is required to be published through iTunes Connect.
* App should be ready for submission and pass the App Store [guidelines](https://developer.apple.com/app-store/review/guidelines/).
* An [Apple ID](https://appleid.apple.com/) without two-factor authentication to manage your Apple account.
* An [Apple Developer Program](https://developer.apple.com/programs/enroll/) account.

For more information, review the [App Distribution Guide](https://developer.apple.com/library/content/documentation/IDEs/Conceptual/AppDistributionGuide/Introduction/Introduction.html#//apple_ref/doc/uid/TP40012582-CH1-SW1).

## Set up the connection between App Center to iTunes and TestFlight

1. Select **Stores** under Distribution. 
2. Click on **Add Connection** in the upper-right corner.
3. Select the store type as **iTunes Connect** from the menu. 
4. Click on **Next** in the lower-right corner.
5. Login with your Apple developer account (a onetime activity) and click **Connect**.
6. On successful login, if the Apple account is a member of multiple teams an option to select the team to associate the builds will be available. If the Apple account is a member of only a single team, then the selection is defaulted to the single one available.
7. Now a list of apps for the team selected will be available for selection.
8. Select to app to be upgraded.
9. Store connections for the selected app will be automatially set up
   * An App Store connection named **Production**.
   * A [TestFlight](https://developer.apple.com/testflight/) connection for internal testers named **iTunes Connect users**. 
   * External tester groups connections based on the external groups created in the iTunes Connect console. 

10. Setting up this connection is a one time process for an app in App Center.

## Publish an iOS package to the App Store (Production)

1. From the Stores home page select the “Production” store created above.
2. Click on **Publish to Store** in the upper-right corner.
3. Upload the iOS app package following [Apples guidelines](https://developer.apple.com/app-store/submissions/)
4. When the package has been uploaded, you should be able to see some details of the application. Click **Next**.
5. Click on **Publish**. The status for this release on the store details page will show as **Submitted**. 
6. Once App Center has completed the hand-over of the app to iTunes, the status of the app will change to **Published**.
7. In case of a failure while publishing by Apple, the status on the store details page will change to **Failed** with the appropriate error message. 
   Review Apple's [app review](https://developer.apple.com/support/app-review/) process.

## Publish an iOS package to TestFlight (Internal Testers)    

1. From the Stores home page select “iTunes Connect users”. 
2. Click on **Publish to Store** in the upper-right corner.
3. Upload the iOS app package following [Apple's guidelines for store submission](https://developer.apple.com/app-store/submissions/). 
4. When the package has been uploaded, you should be able to see some details of the application. Click **Next**.
5. Click on **Publish** to push the app to the **iTunes Connect users** group in TestFlight. The status for this release on the store details page will show as **Submitted**. 
6. Once App Center has completed the hand-over of the app to TestFlight, the status of the app will change to **Published**.
7. In case of a failure while publishing by Apple, the status will change to **Failed** with the appropriate error message.

## Publish an iOS package to TestFlight (External Testers)    

1. From the Stores home page select the external group to distribute to. 
2. Click on **Publish to Store** in the upper-right corner.
3. Upload the iOS app package. 
4. When the package has been uploaded, you should be able to see some details of the application. Click **Next**.
5. Click on **Publish** to push the app to the external group store. The status for this release on the store details page will show as **Submitted**. 
6. Once App Center has completed the hand-over of the app to TestFlight, the status of the app will change to **Published**.
7. In case of a failure with publishing by Apple, the status will change to **Failed** with the appropriate error message.


## Note

Currently when submitting the deliver file to iTunes Connect, App Center is defaulting certain parameters as below:
```javascript
 add_id_info_uses_idfa: false
 export_compliance_uses_encryption: false
 export_compliance_encryption_updated: false
 ```

## Adding Two-factor authentication

After adding an Apple account with two-factor authentication to the Secret Storage, you can additionally add an App-specific password to your account by navigating to [Developer accounts in your Account settings](https://appcenter.ms/settings/accounts).

* Only App Store and Testflight require an app-specific password.
* Only Apple IDs with two-factor authentication enabled can select **Update app-specific password**.

1. Hover over an item in the **Accounts** list.
2. Click the three vertical dots on the right side of the list
3. Select **Update app-specific password**.
4. Generate an app-specific password using the [Apple ID portal](https://appleid.apple.com/), and the name is for your benefit so that you remember which service or app is using the app-specific password.
5. Copy the generated app-specific password and paste it into the dialogue.
6. Save by clicking **Update**.
