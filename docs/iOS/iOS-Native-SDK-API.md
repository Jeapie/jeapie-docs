#iOS Native SDK API
##List of Methods

* [initWithLaunchOptions](#initwithlaunchoptions)
* [registerForPushNotifications](#registerforpushnotifications)
* [sendTag](#sendtag)
* [sendTags](#sendtags)
* [getTags](#gettags)
* [deleteTag](#deletetag)
* [deleteTags](#deletetags)
* [~~sendPurchase~~](#sendpurchase)
* [IdsAvailable](#idsavailable)

##List of Block Callbacks

* [JeapieHandleNotificationBlock](#Jeapiehandlenotificationblock)
* [JeapieResultSuccessBlock](#Jeapieresultsuccessblock)
* [JeapieFailureBlock](#Jeapiefailureblock)
* [JeapieIdsAvailableBlock](#Jeapieisavailableblock)

##Methods
#####**initWithLaunchOptions**

Must be called from `didFinishLaunchingWithOptions` in `AppDelegate.m`. Instead of passing in appId here you can also add Jeapie_APPID as a key in your plist file and place your Jeapie app Id as a value there.

* **Parameters**

 * **`NSDictionary*`** ***launchOptions*** - launchOptions that you received from didFinishLaunchingWithOptions
 * **`NSString*`** ***appId*** - Your Jeapie app id found on the settings page at [jeapie.com](https://jeapie.com).
 * **`JeapieHandleNotificationBlock`** ***callback(Optional)*** - Function to be called when a notification is opened or received while the app is in use.
 * **`BOOL`** ***autoRegister(Optional)*** - Default true. Automatically show the iOS system prompt to accept push notifications. You can pass in false to delay this pop-up and then call `registerForPushNotifications` to prompt them later.

* **Example**

`Objective-C`
```Objective-C
- (BOOL)application:(UIApplication*)application didFinishLaunchingWithOptions:(NSDictionary*)launchOptions {
        self.Jeapie = [[Jeapie alloc] initWithLaunchOptions:launchOptions handleNotification:^(NSString* message, NSDictionary* additionalData, BOOL isActive) {
        }];
  }
```

`Swift`
```Swift
func application(application: UIApplication, didFinishLaunchingWithOptions launchOptions: [NSObject: AnyObject]?) -> Bool {
        let Jeapie: Jeapie = Jeapie(launchOptions: launchOptions) {
          (message, additionalData, isActive) in
        }
}
```

#####**registerForPushNotifications**

Call when you want to prompt the user to accept push notifications. Only call once and only if you passed false to `initWithLaunchOptions autoRegister:`.
* **Example**

`Objective-C`
```Objective-C
[Jeapie registerForPushNotifications];
```

`Swift`
```Swift
Jeapie.registerForPushNotifications();
```

#####**sendTag**

Tag a user based on an app event of your choosing so later you can create segments on [jeapie.com](https://jeapie.com) to target these users. Recommend using sendTags over sendTag if you need to set more than one tag on a user at a time.

* **Parameters**
 * **`NSString*`** ***key*** - Key of your choosing to create or update.
 * **`NSString*`** ***value*** - Value to set on the key.
   * *NOTE*: Passing in a blank String deletes the key, you can also call deleteTag or deleteTags.
 * **`JeapieResultSuccessBlock`** ***onSuccess(Optional)*** - Call if there were no errors sending the tag.
 * **`JeapieFailureBlock`** ***onFailure(Optional)*** - Called if there was an error.
* **Example**

`Objective-C`
```Objective-C
[Jeapie sendTag:@"key" value:@"value"];
```

`Swift`
```Swift
Jeapie.sendTag("key", value: "value");
```

#####**sendTags**

Tag a user based on an app event of your choosing so later you can create segments on [jeapie.com](https://jeapie.com/) to target these users.

* **Parameters**
 * **`NSDictionary*`** ***keyValues*** - Key value pairs of your choosing to create or update.
   * *NOTE*: Passing in a blank `NSString*` as a value deletes the key, you can also call `deleteTag` or `deleteTags`.
 * **`JeapieResultSuccessBlock`** ***onSuccess(Optional)*** - Call if there were no errors sending the tag.
 * **`JeapieFailureBlock`** ***onFailure(Optional)*** - Called if there was an error.
* **Example**

`Objective-C`
```Objective-C
[Jeapie sendTags:(@{@"key1" : @"value1", @"key2" : "value2"}];
```

`Swift`
```Swift
Jeapie.sendTags(["key1": "value1", "key2": "value2");
```


#####**getTags**

Retrieve a list of tags that have been set on the user from the Jeapie server.

* **Parameters**
 * **`JeapieResultSuccessBlock`** ***successBlock*** - Called when tags are received from Jeapie's server.
 * **`JeapieFailureBlock`** ***onFailure(Optional)*** - Called if there was an error.
* **Example**

`Objective-C`
```Objective-C
[Jeapie getTags:^(NSDictionary* tags) {
  NSLog(@"%@", tags);
}];
```

`Swift`
```Swift
Jeapie.getTags({ (tags) in
  NSLog("%@", tags);
});
```

#####**deleteTag**

Deletes a tag that was previously set on a user with `sendTag` or `sendTags`. Use `deleteTags` if you need to delete more than one.

* **Parameters**
 * **`NSString*`** ***key*** - Key to remove.
 * **`JeapieResultSuccessBlock`** ***onSuccess(Optional)*** - Call if there were no errors.
 * **`JeapieFailureBlock`** ***onFailure(Optional)*** - Called if there was an error.
* **Example**

`Objective-C`
```Objective-C
[Jeapie deleteTag:@"key"];
```

`Swift`
```Swift
Jeapie.deleteTag("key");
```

#####**deleteTags**

Deletes tags that were previously set on a user with `sendTag` or `sendTags`.

* **Parameters**
 * **`NSArray*`** ***keys*** - Keys to remove.
 * **`JeapieResultSuccessBlock`** ***onSuccess(Optional)*** - Call if there were no errors.
 * **`JeapieFailureBlock`** ***onFailure(Optional)*** - Called if there was an error.
* **Example**

`Objective-C`
```Objective-C
[Jeapie sendTags:@[@"key1", @"key2"]];
```

`Swift`
```Swift
Jeapie.sendTags(["key1", "key2"]);
```

#####**~~sendPurchase~~**

This was deprecated in version 1.6.0 as purchases are now automatically tracked for you.

~~Call this method when a user completes an in-app purchase, and provide the amount spent in USD. This can later be used to target free vs paid users when sending a push notification.~~

* ~~**Parameters**~~
 * ~~NSNumber amount - Amount spent in USD.~~
* ~~**Example**~~
```Objective-C
// Method call has no affect.
[Jeapie sendPurchase:[NSNumber numberWithDouble:12.34]];
```

#####**IdsAvailable**

Lets you retrieve the Jeapie user id and push token. Your callback block is called after the device is successfully registered with Jeapie. pushToken will be nil if the user did not accept push notifications.

* **Parameters**
 * **`JeapieIdsAvailableBlock`** ***IdsAvailableBlock*** - Called when the user id is available.
* **Example**

`Objective-C`
```Objective-C
[Jeapie IdsAvailable:^(NSString* userId, NSString* pushToken) {
  NSLog(@"UserId:%@", userId);
  if (pushToken != nil)
    NSLog(@"pushToken:%@", pushToken);
}];
```

`Swift`
```Swift
Jeapie.IdsAvailable({ (userId, pushToken) in
  NSLog("UserId:%@", userId);
  if (pushToken != nil) {
    NSLog("pushToken:%@", pushToken);
  }
});
```

##**Block Callbacks**
#####**JeapieHandleNotificationBlock**

Block for Jeapie methods that gets called when the Jeapie server is contacted successfully.

* **Parameters**
 * **`NSDictionary*`** ***message*** - Visible text the user sees on the push notification itself.
 * **`NSDictionary*`** ***additionalData*** - Key value pairs set on the additional data section on jeapie.com.
   * NOTE: If you set Action Buttons on your notification the actionSelected key will contain the id of the button pressed; "_DEFAULT_" will be the id if the user tapped on the notification itself when buttons were present.
 * **`BOOL`** ***isActive*** - True if user is currently using your app when the notification came in.
* **Example**

`Objective-C`
```Objective-C
  self.Jeapie = [[Jeapie alloc] initWithLaunchOptions:launchOptions handleNotification:^(NSString* message, NSDictionary* additionalData, BOOL isActive) {
          UIAlertView* alertView;

          NSLog(@"APP LOG ADDITIONALDATA: %@", additionalData);

          if (additionalData) {
              // Append AdditionalData at the end of the message
              NSString* displayMessage = [NSString stringWithFormat:@"NotificationMessage:%@", message];

              NSString* messageTitle;
              if (additionalData[@"discount"])
                  messageTitle = additionalData[@"discount"];
              else if (additionalData[@"bonusCredits"])
                  messageTitle = additionalData[@"bonusCredits"];
              else if (additionalData[@"actionSelected"])
                  messageTitle = [NSString stringWithFormat:@"Pressed ButtonId:%@", additionalData[@"actionSelected"]];

              alertView = [[UIAlertView alloc] initWithTitle:messageTitle
                                                     message:displayMessage
                                                    delegate:self
                                           cancelButtonTitle:@"Close"
                                           otherButtonTitles:nil, nil];
          }

          // If a push notification is received when the app is being used it does not go to the notifiction center so display in your app.
          if (alertView == nil && isActive) {
              alertView = [[UIAlertView alloc] initWithTitle:@"Jeapie Message"
                                                     message:message
                                                    delegate:self
                                           cancelButtonTitle:@"Close"
                                           otherButtonTitles:nil, nil];
          }

          // Highly recommend adding app logic around this so the user is not interrupted.
          if (alertView != nil)
              [alertView show];

      }];
```

`Swift`
```Swift
let Jeapie: Jeapie = Jeapie(launchOptions: launchOptions) {
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

#####**JeapieResultSuccessBlock**

Block for Jeapie methods that gets called when the Jeapie server is contacted successfully.

* **Parameters**
 * **`NSDictionary`** ***result*** - The resulting JSON response from the Jeapie server.
* **Example**

`Objective-C`
```Objective-C
[Jeapie getTags:^(NSDictionary* result) {
  NSLog(@"%@", result);
}];
```

`Swift`
```Swift
Jeapie.getTags({ (tags) in
  NSLog("%@", tags);
});
```

#####**JeapieFailureBlock**

Block for Jeapie methods that gets called when the Jeapie server can't be contacted or there was a error in the response.

* **Parameters**
 * **`NSError*`** ***error*** - errorWithDomain == "JeapieError", code == HTTP error code from the Jeapie server, userInfo == JSON Jeapie responded with.
* **Example**
```Objective-C
[self.Jeapie registerDeviceToken:deviceToken onSuccess:^(NSDictionary* results) {
  NSLog(@"Device Registered with Jeapie.");
} onFailure:^(NSError* error) {
  NSLog(@"Error in Jeapie Registration: %@", error);
}];
```

#####**JeapieIdsAvailableBlock**

Lets you retrieve the Jeapie user id and device token. Your block is called after the device is successfully registered with Jeapie.

* **Parameters**
 * **`NSString*`** ***userId***- Jeapie userId is a UUID formatted string.(unique per device per app)
 * **`NSString*`** ***pushToken*** - pushToken is a Apple assigned identifier(unique per device per app).

**NOTE**

Might be `nil` if the user does not accept push notifications for your app or there was a connection issue.

**NOTE 2**

If you disable auto register or the user waits over 30 seconds to say yes to the system prompt then your call back will be called twice. First with just the userId filed and then a 2nd time to with the push token included.

* **Example**

`Objective-C`
```Objective-C
[Jeapie IdsAvailable:^(NSString* userId, NSString* pushToken) {
  NSLog(@"UserId:%@", userId);
  if (pushToken != nil)
    NSLog(@"pushToken:", pushToken);
}];
```

`Swift`
```Swift
Jeapie.IdsAvailable({ (userId, pushToken) in
  NSLog("UserId:%@", userId);
  if (pushToken != nil) {
    NSLog("pushToken:%@", pushToken);
  }
});
```