#Android Native SDK API (2.1.x versions)

##List of Methods

* [init](#init)
* [setAlias](#setAlias)
* [setPhone](#setPhone)
* [setEmail](#setEmail)
* [addTag](#addTag)
* [setTags](#setTags)
* [removeTag](#removeTag)
* [removeTags](#removeTags)
* [unsubscribe](#unsubscribe)
* [subscribe](#subscribe)
* [startLocationTrackingService](#startLocationTrackingService)
* [setLocation](#setLocation)
* [pushDelivered](#pushDelivered)

##Methods

#####**<a name="init">init</a>**

Paste method the code into `Launch Activity` or into class extends `android.app.Application`.

```java
public JeapieAPI init(Context context);
```

**Parameters**

* **`context`** ***Context*** - Application context

**Return**

* **`JeapieAPI`** - JeapieAPI instance

**Example**

```java
@Override
public class TestApp extends Application {
    @Override
    public void onCreate() {
        super.onCreate();
            JeapieAPI.init(getApplicationContext());
    }
}
```



---
<br><br>

#####**<a name="setAlias">setAlias</a>**

Set an alias(user identifier) for each user to target these users.

```java
public static void setAlias(String alias);
```

**Parameters**

* **`alias`** ***String*** - user alias (email or other account identifier).

**Example**

```java
JeapieAPI.setAlias("John Smith");
```

---
<br><br>

#####**<a name="setPhone">setPhone</a>**

Set a user phone number for additional user targeting.

```java
public static void setPhoneNumber(String phone);
```

**Parameters**

* **`phone`** ***String*** - user phone.

**Example**

```java
JeapieAPI.setPhoneNumber("380991111111");
```

---
<br><br>

#####**<a name="setEmail">setEmail</a>**

Set a user phone number for additional user targeting.

```java
public static void setEmail(String email);
```

**Parameters**

* **`email`** ***String*** - user email.

**Example**

```java
JeapieAPI.setEmail("login@example.com");
```

---
<br><br>

#####**<a name="addTag">addTag</a>**

Tags a user based on an app event of your choosing so that later you can 
create segments on Jeapie to target these users. 
We recommend using setTags over addTag if you need to set more than one tag for a user at once.

```java
public static void addTag(String tag);
```

**Parameters**

* **`tag`** ***String*** - tag name.

**Example**

```java
JeapieAPI.addTag("tag_name_1");
```

---
<br><br>

#####**<a name="setTags">setTags</a>**

Tags a user based on an app event of your choosing so later 
you can create segments on Jeapie to target these users. ***Remove all tags and set new array of tags.***

```java
public static void setTags(String[] tags);
```

**Parameters**

* **`tags`** ***String[]*** - array of tags.

**Example**

```java
JeapieAPI.setTags(new String[]{"tag_name_1", "tag_name_2"});
```

---
<br><br>

#####**<a name="removeTag">removeTag</a>**

Deletes a tag that was previously set for a user with addTag or setTags. 
Use removeAllTags if you need to delete all of them.

```java
public static void removeTag(String tag);
```

**Parameters**

* **`tag`** ***String*** - tag name.

**Example**

```java
JeapieAPI.removeTag("tag_name_1");
```

---
<br><br>

#####**<a name="removeTags">removeTags</a>**

Deletes all tags that were previously set for a user with addTag or setTags.

```java
public static void removeTags();
```

**Example**

```java
JeapieAPI.removeTags();
```

---
<br><br>

#####**<a name="unsubscribe">unsubscribe</a>**

Unsubscribe this device from push notifications.

```java
public static void unsubscribe();
```

**Example**

```java
JeapieAPI.unsubscribe();
```

---
<br><br>

#####**<a name="subscribe">subscribe</a>**

Subscribe this device to push notifications if it was unsubscribed by `unsubcribe` method.

```java
public static void subscribe();
```

**Example**

```java
JeapieAPI.subscribe();
```

---
<br><br>

#####**<a name="startLocationTrackingService">startLocationTrackingService</a>**

Collect user coordinates for advanced user targeting. Geolocations collect with custom period in seconds 
when mobile application has foreground state.

```java
public static void startLocationTrackingService();
```

**Example**

```java
JeapieAPI.startLocationTrackingService();
```

---
<br><br>

#####**<a name="setLocation">setLocation</a>**

Save user geolocation to Jeapie for advanced user targeting.

```java
public static void setLocation(Double[] longitudeLatitude);
```

**Parameters**

* **`longitudeLatitude`** ***Double[]*** - array of longitude and latitude.

**Example**

```java
JeapieAPI.setLocation(Double[]{45.678, 23.456})l
```

---
<br><br>

#####**<a name="pushDelivered">pushDelivered</a>**

To track the push has been delivered. 

```java
static static void pushDelivered(String pushId, Context context);
```

**Parameters**

* **`pushId`** ***String*** - id of push from push payload.
* **`context`** ***Context*** - context of application.

**Example**

```java
final String pushId = intent.getStringExtra(MESSAGE_ID_EXTRA_FIELD);
JeapieAPI.pushDelivered(pushId, context);
```

---
<br><br>