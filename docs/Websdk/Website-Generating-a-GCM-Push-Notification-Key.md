#Generating a GCM Push Notification Key for Website

###STEP 1: Create a Google Project and save the "Project Number"

**1.1** Create a project at [https://console.developers.google.com/project](https://console.developers.google.com/project) for your app.

![Create project](/img/2015-06-02_1211.png)

**1.2** Select your Project and click on "Overview". Your project number should be located on this page.

![Copy project number](/img/2015-06-02_1222.png)

**Copy the "Project Number" from this page.**

You will need to add it to the source code of your app later when you follow the SDK guide.

###STEP 2: Turn on "Google Cloud Messaging for Android" API

**2.** Under APIs & auth>APIs, search for "Google Cloud Messaging for Android". Turn it on.

![Turn on Google Cloud Messaging](/img/2015-06-02_1225.png)
![Enable API](/img/2015-06-02_1228.png)

###STEP 3: Create and save Server Key

**3.1** Under "APIs & auth" > "Credentials", click "Create new key".

**3.2** Select "Server key"

![Create New key](/img/2015-06-02_1229.png)
![Server key](/img/2015-06-02_1217.png)

**3.3** Press the "Create" button.

**IMPORTANT**

DO NOT enter anything into the box.

![Leave empty](/img/2015-06-02_1218.png)

**3.4** Copy the "API Key". You will need it to configure your project using Jeapie

![Copy API KEY](/img/2015-06-02_1220.png)

###STEP 4: Send your GCM credentials to Jeapie support

**4.1** Send your Project Number and GCM browser key to <a href="mailto:support@jeapie.com">support@jeapie.com</a>.
