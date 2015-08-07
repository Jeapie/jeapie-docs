#iOS Native SDK Installation

###1. Download latest Jeapie iOS sdk from github
[https://github.com/Jeapie/jeapie-ios](https://github.com/Jeapie/jeapie-ios)

###2. Copy folder `jeapie` into root of your ios mobile app

###3. Select "Build Phases" and go to "Link Binary With Libraries".

![Link Binary With Libraries](/img/2015-08-06_1620.png)

You should see jeapie-sdk-x.x.x.a library

###4. Add "-ObjC" linker flag to "Other Linker Flags" in Build Settings 

![Link Binary With Libraries](/img/2015-08-06_1625.png)

###5. Add APP_KEY and APP_SECRET to info.plist

**5.1** Open info.plist as a Source file

![alt text](/img/2015-08-07_1656.png)

**5.2** Take `APP_KEY` and `APP_SECRET` keys from Step 3 *Add Jeapie sdk to your Mobile Application* in Jeapie Dashboard.

![alt text](/img/2015-08-07_1700.png)

**5.3** Paste xml into info.plist

```xml
<key>Jeapie</key>
<dict>
    <key>APP_KEY</key>
    <string>{PASTE_APP_KEY_FROM_JEAPIE_DASHBOARD}</string>
    <key>APP_SECRET</key>
    <string>{PASTE_APP_SECRET_FROM_JEAPIE_DASHBOARD}</string>
</dict>
```

![alt text](/img/2015-08-07_1653.png)

###6. Import Jeapie header file in AppDelegate.m

```objective-c
#import "jeapie/JBJeapieAPIService.h"
```

***Warning!*** *Путь к JBJeapieAPIService.h зависит от того, куда вы сохранили папку `jeapie` в вашем проекте.*

###7. Add a couple of lines in AppDelegate.m

```objective-c
- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions { 
   
    // Enable Push notification   
    // support iOS7 and iOS8 push notifications
    if ([application respondsToSelector:@selector(registerUserNotificationSettings:)]) {
        UIUserNotificationSettings* notificationSettings = [UIUserNotificationSettings settingsForTypes:UIUserNotificationTypeAlert | UIUserNotificationTypeBadge | UIUserNotificationTypeSound categories:nil];
        [[UIApplication sharedApplication] registerUserNotificationSettings:notificationSettings];
        [[UIApplication sharedApplication] registerForRemoteNotifications];
    } else {
        [[UIApplication sharedApplication] registerForRemoteNotificationTypes: (UIRemoteNotificationTypeBadge | UIRemoteNotificationTypeSound | UIRemoteNotificationTypeAlert)];
    }
    
    // track push open
    NSDictionary* userInfo = [launchOptions objectForKey:UIApplicationLaunchOptionsRemoteNotificationKey];
    if (userInfo) {
        [[JBJeapieAPIService sharedInstance] didReceiveRemoteNotification:userInfo];
    }
    
    return YES;
}

// get device token
- (void)application:(UIApplication*)application didRegisterForRemoteNotificationsWithDeviceToken:(NSData*)deviceToken
{
    [[JBJeapieAPIService sharedInstance] didRegisterForRemoteNotificationsWithDeviceToken:deviceToken];
}

// track push opens
- (void)application:(UIApplication *)application didReceiveRemoteNotification:(NSDictionary *)userInfo
{
    [[JBJeapieAPIService sharedInstance] didReceiveRemoteNotification:userInfo];
}
```

###8. Next step use Jeapie SDK API 