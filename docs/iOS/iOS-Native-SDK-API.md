#iOS Native SDK API
##List of Methods

* [didRegisterForRemoteNotificationsWithDeviceToken](#didRegisterForRemoteNotificationsWithDeviceToken)
* [didReceiveRemoteNotification](#didReceiveRemoteNotification)
* [setAlias](#setAlias)
* [setPhone](#setPhone)
* [setEmail](#setEmail)
* [addTag](#addTag)
* [setTags](#setTags)
* [removeTag](#removeTag)
* [removeTags](#removeTags)
* [unsubscribe](#unsubscribe)
* [subscribe](#subscribe)
* [enableGeolocationWithInterval](#enableGeolocationWithInterval)
* [disableGeolocation](#disableGeolocation)
* [setLocation](#setLocation)
* [deliver](#deliver)


##Methods
#####**<a name="didRegisterForRemoteNotificationsWithDeviceToken">didRegisterForRemoteNotificationsWithDeviceToken</a>**

Must be called from `didRegisterForRemoteNotificationsWithDeviceToken` <br>and `didFinishLaunchingWithOptions` in `AppDelegate.m`. 
Register device token in Jeapie Dashboard.

```Objective-C
- (void)didRegisterForRemoteNotificationsWithDeviceToken:(NSData *)data;
```

**Parameters**

* **`NSData*`** ***data*** - device token.

**Example**

`Objective-C`
```Objective-C
- (void)application:(UIApplication*)application didRegisterForRemoteNotificationsWithDeviceToken:(NSData*)deviceToken
{
    [[JBJeapieAPIService sharedInstance] didRegisterForRemoteNotificationsWithDeviceToken:deviceToken];
}
```

---
<br><br>

#####**<a name="didReceiveRemoteNotification">didReceiveRemoteNotification</a>**

Must be called from `didReceiveRemoteNotification` in `AppDelegate.m`. 
Track open push for statistics.

```Objective-C
- (void)didReceiveRemoteNotification:(NSDictionary *)userInfo;
```

**Parameters**

* **`NSDictionary*`** ***userInfo*** - contains  push information.
 
**Example**

`Objective-C`
```Objective-C
- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
    
    // Get push info
    NSDictionary* userInfo = [launchOptions objectForKey:UIApplicationLaunchOptionsRemoteNotificationKey];
    
    if (userInfo) {
        // track push opening
        [[JBJeapieAPIService sharedInstance] didReceiveRemoteNotification:userInfo];
    }
    
    return YES;
}

- (void)application:(UIApplication *)application didReceiveRemoteNotification:(NSDictionary *)userInfo
{
    // track push opening
    [[JBJeapieAPIService sharedInstance] didReceiveRemoteNotification:userInfo];
}
```

---
<br><br>

#####**<a name="setAlias">setAlias</a>**

Set an alias(user identifier) for each user to target these users.

```Objective-C
- (void)setAlias:(NSString *)alias;
```

**Parameters**

* **`NSString*`** ***alias*** - user alias.

**Example**

`Objective-C`
```Objective-C
[[JBJeapieAPIService sharedInstance] setAlias:@"user_identification"];
```

---
<br><br>

#####**<a name="setPhone">setPhone</a>**

Set a user phone number for additional user targeting.

```Objective-C
- (void)setPhone:(NSString *)phone;
```

**Parameters**

* **`NSString*`** ***phone*** - user phone;

**Example**

`Objective-C`
```Objective-C
[[JBJeapieAPIService sharedInstance] setPhone:@"1415111111"];
```

---
<br><br>

#####**<a name="setEmail">setEmail</a>**

Set a user phone number for additional user targeting.

```Objective-C
- (void)setEmail:(NSString *)email;
```

**Parameters**

* **`NSString*`** ***email*** - user email.

**Example**

`Objective-C`
```Objective-C
[[JBJeapieAPIService sharedInstance] setEmail:@"login@example.com"];
```

---
<br><br>

#####**<a name="addTag">addTag</a>**

Tags a user based on an app event of your choosing so that later you can 
create segments on Jeapie to target these users. 
We recommend using setTags over addTag if you need to set more than one tag for a user at once.

```Objective-C
- (void)addTag:(NSString *)tag;
```

**Parameters**

* **`NSString*`** ***tag*** - tag name.

**Example**

`Objective-C`
```Objective-C
[[JBJeapieAPIService sharedInstance] addTag:@"tag_name"];
```

---
<br><br>

#####**<a name="setTags">setTags</a>**

Tags a user based on an app event of your choosing so later 
you can create segments on Jeapie to target these users. ***Remove all tags and set new array of tags.***

```Objective-C
- (void)setTags:(NSArray *)tags;
```

**Parameters**

* **`NSArray*`** ***tags*** - array of tags.

**Example**

`Objective-C`
```Objective-C
[[JBJeapieAPIService sharedInstance] setTags:@[@"tag_name1", @"tag_name2"]];
```

---
<br><br>

#####**<a name="removeTag">removeTag</a>**

Deletes a tag that was previously set for a user with addTag or setTags. 
Use removeAllTags if you need to delete all of them.

```Objective-C
- (void)removeTag:(NSString *)tag;
```

**Parameters**

* **`NSString*`** ***tag*** - tag name.

**Example**

`Objective-C`
```Objective-C
[[JBJeapieAPIService sharedInstance] removeTag:@"tag_name"];
```

---
<br><br>

#####**<a name="removeTags">removeTags</a>**

Deletes all tags that were previously set for a user with addTag or setTags.

```Objective-C
- (void)removeTags;
```

**Example**

`Objective-C`
```Objective-C
[[JBJeapieAPIService sharedInstance] removeTags];
```

---
<br><br>

#####**<a name="unsubscribe">unsubscribe</a>**

Unsubscribe this device from push notifications.

```Objective-C
- (void)unsubscribe;
```

**Example**

`Objective-C`
```Objective-C
[[JBJeapieAPIService sharedInstance] unsubscribe];
```

---
<br><br>

#####**<a name="subscribe">subscribe</a>**

Subscribe this device to push notifications if it was unsubscribed by `unsubcribe` method.

```Objective-C
- (void)subscribe;
```

**Example**

`Objective-C`
```Objective-C
[[JBJeapieAPIService sharedInstance] subscribe];
```

---
<br><br>

#####**<a name="enableGeolocationWithInterval">enableGeolocationWithInterval</a>**

Collect user coordinates for advanced user targeting. Geolocations collect with custom period in seconds 
when mobile application has foreground state.

If you have permission for background geolocation, please use `setLocation` method.


```Objective-C
- (void)enableGeolocationWithInterval:(NSTimeInterval)interval;
```

**Parameters**

* **`NSTimeInterval`** ***interval*** - Interval in seconds. Please use more than 30 sec.

**Example**

`Objective-C`
```Objective-C
[[JBJeapieAPIService sharedInstance] enableGeolocationWithInterval:30];
```

---
<br><br>

#####**<a name="disableGeolocation">disableGeolocation</a>**

Disable collecting user coordinates.

```Objective-C
- (void)disableGeolocation;
```

**Example**

`Objective-C`
```Objective-C
[[JBJeapieAPIService sharedInstance] disableGeolocation];
```

---
<br><br>

#####**<a name="setLocation">setLocation</a>**

Save user geolocation to Jeapie for advanced user targeting.

```Objective-C
- (void)setLocation:(NSArray *)coordinates;
```

**Parameters**

* **`NSArray *`** ***coordinates*** - user coordinates.

**Example**

`Objective-C`
```Objective-C
[[JBJeapieAPIService sharedInstance] setLocation:@[123.21, 321.12]];
```

---
<br><br>

#####**<a name="deliver">deliver</a>**

To track the push has been delivered. *By default we can't check whether push has been delivered, but can use this method 
in specific cases for advanced statistics.*

```Objective-C
- (void)deliver:(NSString *)pushId;
```

**Parameters**

* **`NSString *`** ***pushId*** - 32 symbols push id.

**Example**

`Objective-C`
```Objective-C
[[JBJeapieAPIService sharedInstance] deliver:@"aaaaaaaabbbbbbbbccccccccddddddd"];
```

---
<br><br>


