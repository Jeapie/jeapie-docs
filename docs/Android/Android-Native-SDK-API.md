#Android Native SDK API

##List of Constructors

[Jeapie](#Jeapie)

##List of Methods

* [sendTag](#sendtag)
* [sendTags](#sendtags)
* [getTags](#gettags)
* [deleteTag](#deletetag)
* [deleteTags](#deletetags)
* [sendPurchase](#sendpurchase)
* [IdsAvailable](#idsavailable)
* [onPaused](#onpaused)
* [onResumed](#onresumed)
* [enableVibrate](#enablevibrate)
* [enableSound](#enablesound)

##List of Handler Interfaces

* [NotificationOpenedHandler](#notificationopenedhandler)
* [IdsAvailableHandler](#idsavailablehandler)
* [GetTagsHandler](#gettagshandler)

##Constructors
#####**Jeapie**

You must create a Jeapie instance on the first Android Activity when your app starts. Also make sure you only create one instance and keep the same one around by making it static our assigning it to an object outside of your first Activity. You are also required to override onPaused and onResumed on your Android Activities and call the matching methods on your Jeapie instance.

* Parameters
 * **`Activity`** ***context*** - Pass in your main `Activity` so the api can use it as a `Context`.
 * **`String`** ***google Project Number*** - Your Google project number
 * **`String`** ***Jeapie AppId*** - Your Jeapie app id
 * **`NotificationOpenedHandler`** ***notificationOpenedHandler(Optional)*** - Calls `notificationOpened` on the object when a notification is opened or one is received while the app is running.

**Example**
```Java
public class MainActivity extends Activity {
    @Override
    protected void onCreate(Bundle savedInstanceState) {
      Jeapie = new Jeapie(this, "703322744261", "5eb5a37e-b458-11e3-ac11-000c2940e62c");
    }
  }
```

##Methods

#####**sendTag**

Tag a user based on an app event of your choosing so later you can create segments on [jeapie.com](https://jeapie.com) to target these users. Recommend using sendTags over sendTag if you need to set more than one tag on a user at a time.

* Parameters
 * **`String`** ***key*** - Key of your choosing to create or update.
 * **`String`** ***value*** - Value to set on the key.
   * *NOTE*: Passing in a blank String deletes the key, you can also call deleteTag or deleteTags.

**Example**
```Java
Jeapie.sendTag("key", "value");
```