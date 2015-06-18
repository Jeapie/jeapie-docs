#Website SDK API
**JavaScript Async**

The example assume you have the following defined before calling Jeapie functions:
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

Only required method you need to call to setup Jeapie to receive push notifications. Call this from each page of your site.

* **Parameters**
 * **`JSON`** ***options***
   * **`String`** ***appKey(Required) ***- Your Jeapie app id found on the settings page at jeapie.com.
   * **`Boolean`** ***autoRegister(Optional)*** - Automatically show browser prompt to accept notifications. You can pass in false to delay this pop-up and then call `registerUserForPush` to prompt them later.
   * **`Boolean`** ***createButton(Optional)*** - It creates a default button that, when clicked, the user sees a window for receipt of the notifications
   * **`Boolean`** ***subdomainName(Required for HTTP sites)*** 
   * **`String`** ***tooltipText(Optional, use only with createButton)*** - Default `Подпишитесь на наши обновления в один клик!`. Set text will shown users on deafult button. 

**Example**
```javascript

var Jeapie = Jeapie || [];

Jeapie.init("appKey": "YOUR_JEAPIE_APP_KEY");
```

#####**registerUserForPush**

Call when you want to prompt the user to accept push notifications. Only call if you set false to `autoRegister:` when calling init.

**Example**
```javascript
Jeapie.registerUserForPush(callback);
```

#####**addTag**

Tag a user based on an app event of your choosing so later you can create segments on [jeapie.com](https://jeapie.com) to target these users. Recommend using setTags over addTag if you need to set more than one tag on a user at a time.

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
Jeapie.setTags({"value1", "value2"});
```

#####**removeTag**

Deletes a tag that was previously set on a user with `addTag` or `setTags`. Use `removeAllTags` if you need to delete all of them.

* **Parameters**
 * **`String`** ***value*** - Value to remove.

**Example**
```javascript
Jeapie.removeTag("value");
```

#####**removeAllTags**

Deletes all tags that were previously set on a user with `addTag` or `setTags`.

**Example**
```javascript
Jeapie.removeAllTags();
```

#####**setAlias**

Set a unique value for each user [jeapie.com](https://jeapie.com) to target these users. 

* **Parameters**
 * **`string`** ***value*** - Value to set.

**Example**
```javascript
Jeapie.setAlias("value");
```

#####**isPushManagerSupported**

Returns true if the current browser viewing the page supports push notifications.

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

