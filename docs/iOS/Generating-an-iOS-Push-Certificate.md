#Generating an iOS Push Certificate

The goals of this section are to provision your app with Apple and grant Jeapie access to manage your notifications.

##1. Try out our Automatic Provisioning Tool

We recently released a tool to automate this process!

Simply follow the directions on this page http://jeapie.com/provisionator then [**continue to Step 4**](#4-upload-your-push-certificate-to-Jeapie).
##OR -- Create Certificate Request Manually

**1.1** Open Keychain Access on your Mac OS X system. It may be located in "Applications" > "Utilities" > "Keychain Access"

**1.2** Select "Keychain Access">"Certificate Assistant">"Request a Certificate From a Certificate Authority..."

![alt text](https://www.filepicker.io/api/file/ducGROb2SjGcG68MJxcT "Logo Title Text 1")

**1.3** Select the "Save to disk" option and enter your information in the required fields. This creates a certification request file that will be used later.

![alt text](https://www.filepicker.io/api/file/CVamtSOyRAuD3wyojCbe "Logo Title Text 1")

##2. Enable Push Notifications and apply the Certification Request to generate Certificate

**2.1** Select your app from the [Apple's Developer](https://developer.apple.com/account/ios/identifiers/bundle/bundleList.action) site and press "Edit"

![alt text](https://www.filepicker.io/api/file/LiQTUkUXSPCU2Sh51T5F "Logo Title Text 1")

**2.2** Scroll down to the bottom and enable Push Notifications and press "Create Certificate..." in either Development or Production.

Here's the difference between each kind of certificate:

* **Sandbox Push Certificate** (Also known as Development) - For sending push notifications to a development version of your app that was built with an Apple Development provisioning profile.

* **Production Push Certificate** - For production builds that are submitted to the app store built with an Apple "App Store" provisioning profile, or for testing push notifications in an Ad-Hoc build built with an Apple "Ad Hoc" provisioning profile.

Basically, you will want to start with a Sandbox (Development) Push Certificate when developing or updating your app. Then before submitting your app built it with an "Ad Hoc" Provisioning Profile and Production Push Certificate and make sure it receives push notifications. Finally, when submitting your app continue using the production push certificate.

![alt text](https://www.filepicker.io/api/file/ih1ejbirT222rPNymaRP "Logo Title Text 1")

**2.3** Press Continue

![alt text](https://www.filepicker.io/api/file/udNn3rNvQICp42L7x9tT "Logo Title Text 1")

**2.4** Press "Choose File..", select the "certSigningRequest" file you saved in step 1, press open, and then press "Generate".

![alt text](https://www.filepicker.io/api/file/2Dt9T1IPROmopwwkyXIj "Logo Title Text 1")

**2.5** Press Download to save your certificate

![alt text](https://www.filepicker.io/api/file/34yniISTLK9MB98bDIBw "Logo Title Text 1")

##3. Creating a Private Key

**3.1** Open the .cer file you downloaded in the last step by double clicking on it in Finder.

![alt text](https://www.filepicker.io/api/file/zzb9Zc0ATPugb4nPC6RQ "Logo Title Text 1")

**3.2** After a few seconds the "Keychain Access" program should pop up. Select Login > Keys then right click on your key in the list and select "Export"

![alt text](https://www.filepicker.io/api/file/zGxZvc7USJuSbnZ7ER7V "Logo Title Text 1")

**3.3** Give the file a unique name and press save. You will have an option to protect the file with a password. If you add a password, you need to enter this same password on Jeapie.


##4. Upload Your Push Certificate to Jeapie

**4.1** From [Jeapie](https://jeapie.com), go to "Application Settings" and press Configure to the right of the Apple Settings.

![alt text](https://www.filepicker.io/api/file/zv82OLnLQ3CwH5VrzIeA "Logo Title Text 1")

**4.2** Select the .p12 you exported along with a password if you added one and press Save.

![alt text](https://www.filepicker.io/api/file/y4tr93uRjiCaU9h6hmwc "Logo Title Text 1")

**Important Requirement!**

You must make sure `**Push Notifications**` are enabled on your provisioning profiles before building your app! Please fully follow Step 5 below or your users will NOT be subscribed.
##5. Provisioning Profiles

**5.1** On the left to go to All > Provisioning Profiles. Next find any that are for your app and delete them if they do not have Push Notifications in Enabled Services:.

![alt text](https://www.filepicker.io/api/file/gc0o1oiYRQSC6tCNNHLf "Logo Title Text 1")

**5.2** Recreate the ones you need by pressing the "+" button on the upper right.

![alt text](https://www.filepicker.io/api/file/3ILHQj3jQoa8k6nVTphD "Logo Title Text 1")

**5.3** Re-sync your Developer Account in Xcode by going to Xcode > Preferences... then click on the "View Details..." button. Lastly, click the refresh button on the bottom left of the popup. See [Apple's documentation](https://developer.apple.com/library/mac/recipes/xcode_help-accounts_preferences/articles/obtain_certificates_and_provisioning_profiles.html) for more detailed instructions.

**Congratulations! Jeapie is now setup to push out notifications to your app!**

Next, install the Jeapie SDK in your app.
* Next step for [Native iOS](iOS-Native-SDK-Installation.md)

**TROUBLESHOOTING**

If you are running into any issues you can try troubleshooting them with our [Common Problems Guide]().