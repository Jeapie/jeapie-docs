#Website - Generating a GCM Push Notification Key
######Connect your Google Cloud Messenger enabled website with Jeapie

##STEP 1: Create a Google Project and save the "Project Number"

**1.1** Create a project at https://console.developers.google.com/project for your app.

![alt text](https://www.filepicker.io/api/file/zgNztrTOitXVahPBuKig "Logo Title Text 1")


**1.2** Select your Project and click on "Overview". Your project number should be located on this page.

![alt text](https://www.filepicker.io/api/file/8ePjSw9SfeY0JOqdtcYQ "Logo Title Text 1")

**Copy the "Project Number" from this page.**

You will need to enter this into your app later when you follow the SDK guide.

##STEP 2: Turn on both "Google Cloud Messaging for Chrome" and "Google Cloud Messaging for Android" APIs

**2.** Under APIs & auth>APIs, find "Google Cloud Messaging for Chrome." Turn it on. You will need this for desktop notifications.

Find "Google Cloud Messaging for Android" and turn it on. You need this so that an Android Chrome browser can send system notifications to an Android user.

![alt text](https://www.filepicker.io/api/file/AnU9BiUER0J0RSNECVBw "Logo Title Text 1")
![alt text](https://www.filepicker.io/api/file/lKDf6HaRTsyvLkr00KBo "Logo Title Text 1")

##STEP 3: Create and save Server Key

**3.1** Under "APIs & auth" > "Credentials", click "Create new key".

![alt text](https://www.filepicker.io/api/file/L0jaN5VoSeKYBy99Ymj9 "Logo Title Text 1")

**3.2** Select "Server key".

![alt text](https://www.filepicker.io/api/file/6OWq5lpOTXeclIuVbaYL "Logo Title Text 1")

**3.3** Press the "Create" button.

**IMPORTANT**

DO NOT enter anything into the box.

![alt text](https://www.filepicker.io/api/file/G1Geg5tRsavRrDLbjVOz "Logo Title Text 1")

**3.4** Copy the "API Key". You will need it to configure your project using Jeapie

![alt text](https://www.filepicker.io/api/file/MDZjch1bSdOiZY949Y1i "Logo Title Text 1")

##STEP 4: Configure your Chrome Website with Jeapie

**4.1** Log into Jeapie. In the dashboard, select "Application Settings" then press the "Configure" button to the right of "Chrome Website (GCM)".

**4.2** Paste your Google API Key in here and press Save.

![alt text](https://www.filepicker.io/api/file/0tsQeMpwSyekQNsE1ecg "Logo Title Text 1")
![alt text](https://www.filepicker.io/api/file/lMNSiuzgSieBYH1pDbSS "Logo Title Text 1")

**Configuration for sending Chrome Website push notifications is complete!**

Next step is setting up the Chrome Website SDK

* Follow our [Website SDK HTTPS Installation](Website-SDK-HTTPS-Installation.md) guide if your website uses an HTTPS connection.
* Or follow our [Website SDK HTTP Installation](Website-SDK-HTTP-Installation.md) guide if your website is Non-HTTPS. (Uses an HTTP connection).
