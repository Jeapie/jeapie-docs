#Website SDK API
**JavaScript Async**

The example assumes that you have the following code placed defined before calling Jeapie functions:
```HTML
<script src="https://cdn.jeapie.com/jeapiejs/webpush.js" ></script>
<script>var Jeapie = Jeapie || [];</script>
```

##List of Functions

* [init](#init)
* [registerUserForPush](#registeruserforpush)
* [addTag](#addtag)
* [setTags](#settags)
* [removeTag](#removetag)
* [removeAllTags](#removealltags)
* [setAlias](#setalias)
* [isPushManagerSupported](#ispushmanagersupported)
* [getSubscription](#getsubscription)


##Functions
#####**init**

This is the only required method that you need to call for setting up Jeapie to receive push notifications. Call it from each page of your site.

* **Parameters**
 * **`JSON`** ***options***
   * **`String`** ***appKey (Required) ***-Your Jeapie app id can be found on the settings page at jeapie.com.
   * **`Boolean`** ***autoRegister (Optional)*** - Automatically show browser prompt to accept notifications. You can pass in "false" to delay this pop-up and then call `registerUserForPush` to prompt them later.
   * **`Boolean`** ***createButton (Optional)*** -  It creates a default button that generates a window for receipt of the notifications, which appears after clicking
   * **`Boolean`** ***subdomainName (Required for HTTP sites)*** 
   * **`String`** ***tooltipText (Optional, use only with createButton)*** - Default `One click subscription to our newsletter!`. Set the text that will be shown to users on a default button.

**Example**
```javascript

var Jeapie = Jeapie || [];

Jeapie.init("appKey": "YOUR_JEAPIE_APP_KEY");
```

#####**registerUserForPush**

Call it when you want to prompt the user to accept push notifications. Only call if you set "false" in `autoRegister:` when called "init".

**Example**
```javascript
Jeapie.registerUserForPush(callback);
```

#####**addTag**

Tags a user based on an app event of your choosing so that later you can create segments on [jeapie.com](https://jeapie.com) to target these users. Recommend using setTags over addTag if you need to set more than one tag on a user at a time.

* **Parameters**
 * **`string`** ***value*** - Value to set.

**Example**
```javascript
Jeapie.addTag("value");
```

#####**setTags**

Tag a user based on an app event of your choosing so later you can create segments on [jeapie.com](https://jeapie.com) to target these users.

* **Parameters**
 * **`JSON`** ***values*** - Values of your choosing to create.

**Example**
```javascript
Jeapie.setTags(["value1", "value2"]);
```

#####**removeTag**

Deletes a tag that was previously set for a user with `addTag` or `setTags`. Use `removeAllTags` if you need to delete all of them.

* **Parameters**
 * **`String`** ***value*** - Value to remove.

**Example**
```javascript
Jeapie.removeTag("value");
```

#####**removeAllTags**

Deletes all tags that were previously set for a user with `addTag` or `setTags`.

**Example**
```javascript
Jeapie.removeAllTags();
```

#####**setAlias**

Set a alias(user identifier) for each user of [jeapie.com](https://jeapie.com) to target these users. 

* **Parameters**
 * **`string`** ***value*** - Value to set.

**Example**
```javascript
Jeapie.setAlias("value");
```

#####**isPushManagerSupported**

Returns "true" If the browser of current viewer of the page supports push notifications.

```javascript
Jeapie.isPushManagerSupported();
```

#####**getSubscription**

Lets you retrieve the Google Registration ID. Your handler is called after the device is successfully registered with Jeapie.

**Example**
```javascript
Jeapie.getSubscription(function (subscriptionId) {
    if (subscriptionId) {
        console.log(subscriptionId);
    }
});
```

