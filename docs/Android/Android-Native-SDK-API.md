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

#####**sendTags**

Tag a user based on an app event of your choosing so later you can create segments on [jeapie.com](https://jeapie.com/) to target these users.

* Parameters
 * **`JSONObject`** ***keyValues*** - Key value pairs of your choosing to create or update.
   * *NOTE*: Passing in a blank String as a value deletes the key, you can also call deleteTag or deleteTags.

**Example**
```Java
  JSONObject tags = new JSONObject();
  tags.put("key1", "value1");
  tags.put("key2", "value2");
  Jeapie.sendTags(tags);
```

#####**getTags**

Retrieve a list of tags that have been set on the user from the Jeapie server.

* Parameters
 * **`GetTagsHandler`** ***handler*** - Calls `tagsAvailable` on the Object once the tags are available.

**Example**
```Java
Jeapie.getTags(new GetTagsHandler() {
    @Override
    public void tagsAvailable(JSONObject tags) {
      Log.d("debug", tags.toString());
    }
  });
```

#####**deleteTag**

Deletes a tag that was previously set on a user with `sendTag` or `sendTags`. Use `deleteTags` if you need to delete more than one.

* Parameters
 * **`String`** ***key*** - Key to remove.

**Example**
```Java
Jeapie.deleteTag("key");
```

#####**deleteTags**

Deletes tags that were previously set on a user with `sendTag` or `sendTags`.

* Parameters
 * **`Collection<String>`** ***keys*** - Keys to remove.

**Example**
```Java
Collection<String> tempList = new ArrayList<String>();
  tempList.add(key);
  Jeapie.deleteTags(tempList);
```

#####**~~sendPurchase~~**

This was deprecated in version 1.4.0 as Google Play and Amazon (IAP v2) purchases are now automatically tracked for you.

~~Call this method when a user completes an in-app purchase, and provide the amount spent in USD. This can later be used to target free vs paid users when sending a push notification.~~

* ~~Parameters~~
 * ~~(BigDecimal OR double) amount - Amount spent in USD.~~

* ~~Example~~
```Java
// This method call as no affect as purchases are now tracked automatically.
Jeapie.sendPurchase(1.23d);
```

#####**idsAvailable**

Lets you retrieve the Jeapie user id and the Google registration id. Your handler is called after the device is successfully registered with Jeapie.

* Parameters
 * **`IdsAvailableHandler`** ***handler*** - Calls `tagsAvailable` on the Object when the user id is available.

**Example**
```Java
Jeapie.idsAvailable(new IdsAvailableHandler() {
    @Override
    public void idsAvailable(String userId, String registrationId) {
      Log.d("debug", "User:" + userId);
      if (registrationId != null)
        Log.d("debug", "registrationId:" + registrationId);
    }
  });
```

#####**onPaused**

Tells Jeapie that the user is no longer in your app. This is used to track session duration of your app and when to show a notification in the notification area or to just call your `NotificationOpenedHandler`. So make sure to place this and `onResume` in each of your `Activity` classes.

**Example**
```Java
  @Override
  protected void onPause() {
    super.onPause();
    Jeapie.onPaused();
  }
```

#####**onResumed**

Tells Jeapie that the user returned to your app. This is used to track session duration of your app and when to show a notification in the notification area or to just call your `NotificationOpenedHandler`. So make sure to place this and `onPaused` in each of your `Activity` classes.

**Example**
```Java
@Override
  protected void onResume() {
    super.onResume();
    Jeapie.onResumed();
  }
```

#####**enableVibrate**

*You can call this from your UI from a button press for example to give your user's options for your notifications.*

By default Jeapie always vibrates the device when a notification is displayed unless the device is in a total silent mode. Passing false means that the device will only vibrate lightly when the device is in it's vibrate only mode.

**Example**
```Java
Jeapie.enableVibrate(false);
```

#####**enableSound**

*You can call this from your UI from a button press for example to give your user's options for your notifications.*

By default Jeapie plays the system's default notification sound when the device's notification system volume is turned on. Passing false means that the device will only vibrate unless the device is set to a total silent mode.

**Example**
```Java
Jeapie.enableSound(false);
```

##Handler Interfaces
#####**NotificationOpenedHandler**

Interface containing the method `notificationOpened` which you can implement to process information on the notification the user just opened.

#####**notificationOpened**

* Parameters
 * **`String`** ***message*** - The message text the user seen in the notification.
 * **`JSONObject`** ***additionalData*** - Key value pairs that were set on the notification.
 * **`boolean`** ***isActive*** - True if your app was currently being used when a notification came in.

***NOTE***

If you set Action Buttons on your notification, the actionSelected key will contain the id of the button pressed; "__DEFAULT__" will be the id if the user tapped on the notification itself when buttons were present.

**Example**
```Java
@Override
  public static void notificationOpened(String message, JSONObject additionalData, boolean isActive) {
    String messageTitle;
    AlertDialog.Builder builder = null;

    if (additionalData != null) {
      if (additionalData.has("discount"))
        messageTitle = "Discount!";
      else if (additionalData.has("bonusCredits"))
        messageTitle = "Bonus Credits!";
      else
        messageTitle = "Other Extra Data";

      builder = new AlertDialog.Builder(this)
          .setTitle(messageTitle)
          .setMessage(message + "\n\n" + additionalData.toString());
    }
    else if (isActive) // If a push notification is received when the app is being used it does not display in the notification bar so display in the app.
      builder = new AlertDialog.Builder(this)
          .setTitle("Jeapie Message")
          .setMessage(message);

    // Add your app logic around this so the user is not interrupted during gameplay.
    if (builder != null)
      builder.setCancelable(true)
           .setPositiveButton("OK",null)
           .create().show();
  }
```

If want to process a notification before it is clicked or want to handle receiving a silent notification see our [Background Data documentation](Android-Notification-Customizations.md#background-data-silent-notifications).

#####**IdsAvailableHandler**

Interface which you can implement and pass to `Jeapie.idsAvailable` to get the Jeapie userId and the Google registration Id.

#####**IdsAvailable**

* Parameters
 * **`String`** ***userId*** - Jeapie userId is a UUID formatted string.(*unique per device per app*)
 * **`String`** ***registrationId*** - Registration Id is a Google assigned identifier(*unique per device per app and changes on reinstalls*).

**NOTE**

Might be `null` if Google play services are not installed on the device or there was a connection issue.

**Example**
```Java
Jeapie.idsAvailable(new IdsAvailableHandler() {
     @Override
     public void idsAvailable(String userId, String registrationId) {
      Log.d("debug", "User:" + userId);
      if (registrationId != null)
        Log.d("debug", "registrationId:" + registrationId);
     }
  });
```

#####**GetTagsHandler**

Interface which you can implement and pass to `Jeapie.getTags` to get the all the tags set on a user from jeapie.com.

#####**tagsAvailable**

* Parameters
 * **`JSONObject`** ***tags*** - JSONObject of key value pairs retrieved from the Jeapie server

**Example**
```Java
Jeapie.getTags(new GetTagsHandler() {
    @Override
    public void tagsAvailable(JSONObject tags) {
      Log.d("debug","Current Tags on User:" + tags.toString());
    }
  });
```