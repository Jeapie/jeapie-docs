#Android - Generating a GCM Push Notification Key
######Connect your Google Cloud Messenger Android app with Jeapie

##STEP 1: Create a Google Project and save the "Project Number"

**1.1** Create a project at [https://console.developers.google.com/project](https://console.developers.google.com/project) for your app.

![Create project](/img/2015-06-02_1211.png)

**1.2** Select your Project and click on "Overview." Your project number should be located on this page.

![Copy project number](/img/2015-06-02_1222.png)

**Copy the "Project Number" from this page.**

You will need to enter this into your app later when you follow the SDK guide.

##STEP 2: Turn on "Google Cloud Messaging for Android" API

**2.** Under APIs & auth>APIs, search for "Google Cloud Messaging for Android." Turn it on.

![Turn on Google Cloud Messaging](/img/2015-06-02_1225.png)
![Enable API](/img/2015-06-02_1228.png)

##STEP 3: Create and save Server Key

**3.1** Under "APIs & auth" > "Credentials", Click "CREATE NEW KEY".

**3.2** Select "Server key"

![Create New key](/img/2015-06-02_1229.png)
![Server key](/img/2015-06-02_1217.png)

**3.3** Press the Create button.

**IMPORTANT**

DO NOT enter anything into the box.

![Leave empty](/img/2015-06-02_1218.png)

**3.4** Copy the "API Key." You will need it to configure your project with Jeapie

![Copy API KEY](/img/2015-06-02_1220.png)

##STEP 4: Configure your Android App with Jeapie

**4.1** Log into Jeapie. In the dashboard, select "Application Settings" then press the "Configure" button to the right of "Google Play (GCM)".

![Select mobile platform](/img/2015-06-02_1233.png)
![Enter app name](/img/2015-06-02_1235.png)

**4.2** Paste your Google API Key in here and press Save.

![Save android key](/img/2015-06-03_0742.png)

**Configuration to send Android push notifications is complete!**

Next step is to [set up the Android SDK](Android-Native-SDK-Installation.md)