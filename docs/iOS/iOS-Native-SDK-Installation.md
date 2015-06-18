#iOS Native SDK Installation

##1. Import the Jeapie.framework into your Xcode project with CocoaPods.

The recommended way to add the Jeapie library to your project is to use [CocoaPods](https://cocoapods.org/) so it is easier to update. After [setting up CocoaPods](http://guides.cocoapods.org/using/getting-started.html), add `pod 'Jeapie'` to the Podfile. Then, run `pod install`. Lastly make sure to open the .xcworkspace file that CocoaPods creates instead of your original project file. **Skip To Step 2** in this doc.
##OR -- Import the framework manually

Continue reading for directions on how to manually add the [Jeapie library](https://github.com/jeapie/Jeapie-iOS-SDK).

* 1.1 Select "Build Phases" and go to "Link Binary With Libraries".

![alt text](https://www.filepicker.io/api/file/BjJqgZ9LTB2RHHLFXEFh "Logo Title Text 1")

* 1.2 Press the "+" button then search for SystemConfiguration.framework and press Add.

![alt text](https://www.filepicker.io/api/file/xOipHL9nSPm9u0OhkLKr "Logo Title Text 1")

* 1.3 Press the "+" button again then press the "Add Other" button on the bottom. Next select the [Jeapie.framework](https://github.com/jeapie/Jeapie-iOS-SDK) and press Open.

![alt text](https://www.filepicker.io/api/file/Q8zcE8gTxyFzJReJkSIk "Logo Title Text 1")

* 1.4 Add `-ObjC` to "Build Settings">"Other Linker Flags" (Objective-C only)

![alt text](https://www.filepicker.io/api/file/zx7Xv2RjGSp1WA9OzHFw "Logo Title Text 1")

##2. Add Required Capabilities

**3.1** Enable "Background Modes" and check "Remote notifications" under Capabilities on your target.

![alt text](https://www.filepicker.io/api/file/pvXDhthTZ6ZM1OLKnol1 "Logo Title Text 1")

##Add Required Code

**1** If you're using Objective-C, follow the steps in **3A** below.

**2** Otherwise, If you're using Swift, follow the steps in **3B** below.
##3A. Add code to AppDelegate (Objective-C)

**3A.1** In `AppDelegate.h` import `Jeapie/Jeapie.h` and define Jeapie.
```Objective-C
#import <Jeapie/Jeapie.h>
@property (strong, nonatomic) Jeapie *Jeapie;
```

**3A.2** In `AppDelegate.m` add the `didFinishLaunchingWithOptions` method below. Replace "5eb5a37e-b458-11e3-ac11-000c2940e62c" with your Jeapie AppId.

`handleNotification` is optional.

```Objective-C
- (BOOL)application:(UIApplication*)application didFinishLaunchingWithOptions:(NSDictionary*)launchOptions {
    self.Jeapie = [[Jeapie alloc] initWithLaunchOptions:launchOptions
                                        appId:@"5eb5a37e-b458-11e3-ac11-000c2940e62c"
                                        handleNotification:^(NSString* message, NSDictionary* additionalData, BOOL isActive) {
           // This function gets call when a notification is tapped on
           // or one is received while the app is in focus.
        NSString* messageTitle = @"Jeapie Example";
        NSString* fullMessage = [message copy];

        if (additionalData) {
            if (additionalData[@"inAppTitle"])
                messageTitle = additionalData[@"inAppTitle"];

            if (additionalData[@"actionSelected"])
                fullMessage = [fullMessage stringByAppendingString:[NSString stringWithFormat:@"\nPressed ButtonId:%@", additionalData[@"actionSelected"]]];
        }

        UIAlertView* alertView = [[UIAlertView alloc] initWithTitle:messageTitle
                                                            message:fullMessage
                                                           delegate:self
                                                  cancelButtonTitle:@"Close"
                                                  otherButtonTitles:nil, nil];
        [alertView show];

    }];
    return YES;
}
```

##3B. Add Code (Swift)

**3B.1** Add the following import line to your `-Bridging-Header.h`. If you don't have one in your Swift project see [Apple's documentation](https://developer.apple.com/library/ios/documentation/Swift/Conceptual/BuildingCocoaApps/MixandMatch.html#//apple_ref/doc/uid/TP40014216-CH10-XID_79) to add one.
```Swift
#import <Jeapie/Jeapie.h>
```

**3B.2** Open your `AppDelegate.swift` and add the following in your `didFinishLaunchingWithOptions` function. Replace "5eb5a37e-b458-11e3-ac11-000c2940e62c" with your Jeapie AppId.

```Swift
func application(application: UIApplication, didFinishLaunchingWithOptions launchOptions: [NSObject: AnyObject]?) -> Bool {
  let Jeapie: Jeapie = Jeapie(launchOptions: launchOptions, appId: "5eb5a37e-b458-11e3-ac11-000c2940e62c") {
          (message, additionalData, isActive) in
            if (additionalData != nil) {
                NSLog("APP LOG ADDITIONALDATA: %@", additionalData);
                // Append AdditionalData at the end of the message
                let displayMessage: NSString = NSString(format:"NotificationMessage:%@", message);

                var messageTitle: NSString = "";
                if (additionalData["discount"] != nil) {
                    messageTitle = additionalData["discount"] as String
                }
                else if (additionalData["bonusCredits"] != nil) {
                    messageTitle = additionalData["bonusCredits"] as String;
                }
                else if (additionalData["actionSelected"] != nil) {
                    messageTitle = NSString(format:"Pressed ButtonId:%@", additionalData["actionSelected"] as String);
                }

                var alertView: UIAlertView = UIAlertView(title: messageTitle,
                    message:displayMessage,
                    delegate:self,
                    cancelButtonTitle:"Close");

                // Highly recommend adding app logic around this so the user is not interrupted.
                alertView.show();
            }
            // If a push notification is received when the app is being used it does not go to the notifiction center so display in your app.
            else if (isActive) {
                var alertView: UIAlertView = UIAlertView(title:"Jeapie Message",
                    message:message,
                    delegate:self,
                    cancelButtonTitle:"Close");
                alertView.show();
            }
        }
```

**That's it for the Xcode setup!**

The Xcode simulator doesn't support push notifications so you must test on a device. If you haven't done so already make sure your [iOS certificate is configured in Jeapie](Generating-an-iOS-Push-Certificate.md) so you can send notifications out.
iOS SDK API

To see all available methods, see our [iOS Native API Documentation](iOS-Native-SDK-API.md).
