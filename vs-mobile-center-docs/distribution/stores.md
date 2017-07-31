---
title: Use CodePush to update your app live
description: Fix bugs and add content quickly
keywords: distribution
author: iageoghe
ms.author: iageoghe
ms.date: 06/02/2017
ms.topic: article
ms.assetid: F19F4122-B9F0-42CC-85B8-E3C344AE5419
ms.service: mobile-center
ms.custom: distribute
---

## Google Play Store Distribution 

You can now publish an upgrade to an existing app in Google play store from Mobile Center.

### Google Pre-requisites:

* At-least one version of your application exists in Google Play.
* Google Play Developer account. If you don’t have one, then please register for a Google play developer account at
<https://play.google.com/apps/publish/signup>
* You can log in to access the Google Play Developer Console to publish your first version of your application.
* Mobile center uses the Google API’s to enable users to publish an update. In order for Mobile center to access these API’s on user’s behalf, you need to create a API project and a Service account (if you don’t’ have one). This is an account that belongs to an application instead of the user and will be used in creating the store in Mobile Center

For more information on how to use the Google Play Console please use the following link:
<https://support.google.com/googleplay/android-developer/answer/6112435?hl=en>

## Linking your API Project

Before you can access the API, you must link your Google Play Console to an API project. In most cases, we recommend that you create a new API project, though current API users can link to an existing API project. Keep in mind that each API project can only be linked to a single Google Play Console account.

**Creating a new API project**

* Go to the [API Access](https://play.google.com/apps/publish/#ApiAccessPlace) page on the Google Play Console.
* Accept the Terms of Service.
* Click **Create new project**.
* An API project is automatically generated and linked to your Google Play Console.

**Using an existing API project**

* If you are already a user of the Google Play Developer API, you can link to your existing API project by following these steps. If the API project you want to link to is not listed, verify that your Google Play Console account is designated as an Owner, and the Google Play Developer API is enabled.
* Go to the [API Access](https://play.google.com/apps/publish/#ApiAccessPlace) page on the Google Play Console.
* Accept the API Terms of Service.
* Choose the project you’d like to link.
* Click **Link**.

 Setting Up API Access Clients
------------------------------

### Using a service account

You can also create a [service account](https://developers.google.com/accounts/docs/OAuth2ServiceAccount) to access the API from a build server without providing your personal user credentials:

1. Go to the [API Access](https://play.google.com/apps/publish/#ApiAccessPlace) page on the Google Play Console.

<img src="./images/image1.png" width="497" height="153" />

2. Under **Service Accounts**, click **Create Service Account**.

<img src="./images/image2.png" width="365" height="195" />

3. Follow the instructions on the page to create your service account.

<img src="./images/image3.png" width="343" height="213" />

4. On click of [Google API Console](https://play.google.com/apps/publish/#ApiAccessPlace) link.
    Proceed by clicking **+ CREATE SERVICE ACCOUNT**.

<img src="./images/image4.png" width="544" height="77" />

        - Configure it as:

<img src="./images/image5.png" width="288" height="217" />

    - Choose a name for your Service Account and click **Select a role** drop-down menu. select **Owner** (full access to the integration) under **Project**

<img src="./images/image6.png" width="404" height="242" />

    - Choose a **JSON Key Type**, by clicking on Furnish a new private Key.

<img src="./images/image7.png" width="291" height="273" />

    - Click **Create**, and you are done.

**Note:** As you have chosen a JSON Key Type, a file with a .json extension will be downloaded on your machine. ***You will need this file for publish your application***

5. Once you’ve created the service account on the Google Developers Console, click **Done**. The [API Access](https://play.google.com/apps/publish/#ApiAccessPlace) page
automatically refreshes, and your service account will be listed.

<img src="./images/image8.png" width="503" height="221" />

6. Click **Grant Access** to provide the service account the necessary rights to perform actions.

    At this point, you should be able to access the API through the service account. For more information, see [Using OAuth 2.0 for Server to Server Applications](https://developers.google.com/accounts/docs/OAuth2ServiceAccount).

For more information on this please check out this link:
<https://developers.google.com/android-publisher/getting_started>

**You are now done with the Google required pre-requisites and ready to publish an update to the Play store from Mobile Center**

### Step1: Create a Store in Mobile Center

Now that you have all your account credentials, you can create a Distribution store.

1. Click on **Stores** in Distribution beacon. Click on **Add
    Connection**.

2. Select the store type you want to connect to

3. Select Google Play store and click **Next.**

4. You will need to upload the **Private Key JSON** file which you downloaded to your machine while creating the service account. Please do not edit this JSON file.

**Note:** If the JSON fields are edited to incorrect values, your creation of store might fail. Please make sure you have your service account linked to your Google play Developer console as mentioned in the pre-requisite section above. If not linked, your store creation will fail.

1. Once you upload, click **Connect**.

2. You are now connected, and you should now be able to see a store by the name **GooglePlay-Production** store in the **stores** home page.

### Step 2: Publish to Google Play Store

1. From the **stores** home page click on the Google-Play-Production Distribution Store which you created above.

2. Click on **Publish to store**.

3. Upload the application package and enter release notes (if any).

**Note:**

- Application type should be correct and should be signed with a valid key store before uploading.

- Google Play store supports a maximum of 100 MB of application package. If your application exceeds 100 Mb, use the Expansion files to support the application package by uploading those directly in the google play developer console as we currently don’t support Expansion files in Mobile Center. For more information on Expansion files, check out the link here:   
<https://support.google.com/googleplay/android-developer/answer/2481797?hl=en>

- The version of the .apk must be strictly greater than the current version in production.

- If you have app versions in other tracks like Alpha and Beta, your release version should be strictly less than versions in alpha and Beta track versions

4. Once the package has been uploaded you should be able to see some details of the application. Click **Next** to go to the next page.

5. Click **Publish** to publish this app to the **Google Play store**. Once you click publish, you should be able to see this release on the store details page with status as **Submitted.**

6. Once your app is published, the status of the app will change to **Published.**

7. In case of a failure while publishing the status will change to failed with an appropriate error message. You can reach out via Intercom for help in case of issues.





