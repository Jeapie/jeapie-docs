#Website SDK API
**JavaScript Async**

The example assumes that you have the following code placed defined before calling Jeapie functions:
```HTML
<script src="https://cdn.jeapie.com/jeapiejs/APP_KEY" async></script>
<script>var Jeapie = Jeapie || [];</script>
```
Update `APP_KEY` with your Jeapie AppId.

##List of Functions

* [init](#init)
* [registerUserForPush](#registeruserforpush)
* [addTag](#addtag)
* [setTags](#settags)
* [removeTag](#removetag)
* [removeAllTags](#removealltags)
* [setAlias](#setalias)
* [getSubscription](#getsubscription)afterSubscription
* [afterSubscription](#aftersubscription)isSubscribed
* [isSubscribed](#issubscribed)

##Functions
#####**init**

This is the only required method that you need to call for setting up Jeapie to receive push notifications. Call it from each page of your site.

* **Parameters**
 * **`JSON`** ***options***
   * **`Boolean`** ***autoRegister (Optional)*** - Automatically show browser prompt to accept notifications. You can pass in "false" to delay this pop-up and then call `registerUserForPush` to prompt them later.
   * **`Boolean`** ***createButton (Optional)*** -  It creates a default button that generates a window for receipt of the notifications, which appears after clicking
   * **`String`** ***tooltipText (Optional, use only with createButton)*** - Default `One click subscription to our newsletter!`. Set the text that will be shown to users on a default button.

**Example**
```javascript

var Jeapie = Jeapie || [];

Jeapie.push(["init", {"autoRegister":false}]);
```

#####**registerUserForPush**

Call it when you want to prompt the user to accept push notifications. Only call if you set "false" in `autoRegister:` when called "init".

**Example**
```javascript
var Jeapie = Jeapie || [];
Jeapie.push(["registerUserForPush", callback]);
```

#####**addTag**

Tags a user based on an app event of your choosing so that later you can create segments on [jeapie.com](https://jeapie.com) to target these users. Recommend using setTags over addTag if you need to set more than one tag on a user at a time.

* **Parameters**
 * **`string`** ***value*** - Value to set.

**Example**
```javascript
var Jeapie = Jeapie || [];
Jeapie.push(["addTag", "value"]);
```

#####**setTags**

Tag a user based on an app event of your choosing so later you can create segments on [jeapie.com](https://jeapie.com) to target these users.

* **Parameters**
 * **`JSON`** ***values*** - Values of your choosing to create.

**Example**
```javascript
var Jeapie = Jeapie || [];
Jeapie.push(["setTags", ["value1", "value2"] ]);
```

#####**removeTag**

Deletes a tag that was previously set for a user with `addTag` or `setTags`. Use `removeAllTags` if you need to delete all of them.

* **Parameters**
 * **`String`** ***value*** - Value to remove.

**Example**
```javascript
var Jeapie = Jeapie || [];
Jeapie.push(["removeTag", "value"]);
```

#####**removeAllTags**

Deletes all tags that were previously set for a user with `addTag` or `setTags`.

**Example**
```javascript
var Jeapie = Jeapie || [];
Jeapie.push(["removeAllTags"]);
```

#####**setAlias**

Set a alias(user identifier) for each user of [jeapie.com](https://jeapie.com) to target these users. 

* **Parameters**
 * **`string`** ***value*** - Value to set.

**Example**
```javascript
var Jeapie = Jeapie || [];
Jeapie.push(["setAlias", "value"]);
```

#####**getSubscription**

Lets you retrieve the Google Registration ID. Your handler is called after the device is successfully registered with Jeapie.

**Example**
```javascript
var Jeapie = Jeapie || [];
Jeapie.push(["getSubscription", function (subscriptionId) {
    if (subscriptionId) {
        console.log(subscriptionId);
    }
}]);
```

#####**afterSubscription**

Callback that is called after the device is successfully registered with Jeapie. Return `Google Registration ID`.

**Example**
```javascript
var Jeapie = Jeapie || [];
Jeapie.push(["afterSubscription", function (token) {
    console.log(token);
    //Your action
}]);
```

#####**isSubscribed**

Shows if user give permission to send notifications. Return `true` or `false`

**Example**
```javascript
var Jeapie = Jeapie || [];
Jeapie.push(["isSubscribed", function (success) {
    console.log(success);
    //Your action
}]);
```

