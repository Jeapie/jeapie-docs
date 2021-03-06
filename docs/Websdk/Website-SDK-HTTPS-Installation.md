#Website SDK HTTPS Installation
######Jeapie SDK Installation for Chrome websites (desktop + mobile)

**Requirements**

W3C Web Push Notifications are currently only supported by Chrome 42+

* Includes Chrome for Windows, Mac OS X, Linux, Chrome OS, and Android. Chrome for iOS is not yet supported.

**HTTP and HTTPS**

If some of your pages are served via HTTP instead of HTTPS, then you will need to follow our [HTTP Installation Guide](Website-SDK-HTTP-Installation.md) instead.

If possible, we encourage you to migrate all your pages to HTTPS first, and then continue using this guide.

##1. Download the SDK

**1.1** Download the latest version of Jeapie Chrome Web SDK after the registration of your site in the  [Jeapie Dashboard](https://go.jeapie.com/app/step1-add-site-name).

**1.2** Copy `push-worker.js` and `manifest.json` from `jeapie_sdk_` directory and paste it into the top-level directory (root folder) of your site.

##2. Include Required Files

**2.1** Link `https://cdn.jeapie.com/jeapiejs/APP_KEY` and `manifest.json` to each page of your website by adding some code between `<head>` and `</head>` tags. Update `APP_KEY` with your Jeapie AppId.  Most likely, you will have to do it just once in the file, which helps to generate a layout of the site. The resulting HTML should look like this:
```HTML
<head>
	<script src="https://cdn.jeapie.com/jeapiejs/APP_KEY" async></script>
</head>
```
Now user will see a window asking for permission to receive notifications from your site immediately after opening the page

![Autoregister for users](/img/https_autoregister.png)

##3. Customize Jeapie (Optional)

**3.1 Your custom button or event.** 

Call `Jeapie.push(["init"])` from a javascript file that is included in every page. Create or use your button and update `YOUR_CUSTOM_BUTTON_ID` with your button id
```javascript
var Jeapie = Jeapie || [];
Jeapie.push(["init", {"autoRegister":false}]);

window.onload = function(){
	//Replace YOUR_CUSTOM_BUTTON_ID with your button id
	document.getElementById("YOUR_CUSTOM_BUTTON_ID").onclick = registerPush;

	function registerPush() {
		Jeapie.push(["registerUserForPush", function(success){
	        if (success) {
	            //your custom action
	        }
	    }]);
	}
}
```
The user will see a window asking for permission to receive notifications from your site immediately after clicking on the button.

You can create your own logic and call `registerPush()` method.

**Important**

You must keep all the SDK files together. `https://cdn.jeapie.com/jeapiejs/APP_KEY`, `push-worker.js` and `manifest.json` must be placed in the root directory of your site.

Link to `https://cdn.jeapie.com/jeapiejs/APP_KEY` must be added between `<head>` and `</head>` tags for every page on your website. Linking files this way allows us to be sure that:
- any page can subscribe to notifications
- any page can be opened from a notification (if set)
- changes to the Google Registration id can be updated
- session count can be accurately calculated


**That's It!**

That’s it for now - the setup is complete. See our [Web SDK API](Website-SDK-API.md) for more functions.
