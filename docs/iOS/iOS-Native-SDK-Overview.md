#iOS Native SDK Overview
To get Jeapie Push Notifications running on iOS follow two steps:

##Step 1: Generate an iOS Push Certificate

[Generate an iOS Push Certificate](Generating-an-iOS-Push-Certificate.md)

**What are iOS Push Certificates?**

The Apple Push Notification Service (APNs) is a service created by Apple Inc. way back in 2009 to securely send push notifications from third party apps to their users' Apple devices.

Your backend sends notifications through Apple's servers to your application. To ensure that unwanted parties are not sending notifications to your application, Apple needs to know that only your servers can connect with theirs.

Apple, therefore, requires you to create an SSL certificate. Although app provisioning can be confusing at times, follow along and it'll only take two minutes.

##Step 2: Install the Jeapie iOS SDK

[Install the Jeapie iOS SDK](iOS-Native-SDK-Installation.md)