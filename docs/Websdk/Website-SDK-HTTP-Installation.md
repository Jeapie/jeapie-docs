#Website SDK HTTP Installation
Jeapie SDK Installation for Chrome websites (desktop + mobile)

**HTTP vs. HTTPS**

This is the guide for using Google Chrome push notifications on websites that have some pages served via HTTP instead of HTTPS.

If you are sure that each page is served only via HTTPS, then you should follow [this guide] (Website-SDK-HTTPS-Installation.md)

**Requirements**

W3C Web Push Notifications are currently only supported by Chrome 42+

* Includes Chrome for Windows, Mac OS X, Linux, Chrome OS and Android. Chrome for iOS is not yet supported by Google.

#1. Include Required JeapieSDK.js

**1.1** Include `https://cdn.jeapie.com/jeapiejs/APP_KEY` in the the `<head>` HTML tag of each of your website pages. Update `APP_KEY` with your Jeapie AppId. The best way is to add it to the code that generates the layout for each of your webpages. The resulting HTML should look like this:
```HTML
<head>
	<script src="https://cdn.jeapie.com/jeapiejs/c98ddb5b4e54032b1f012127a3c5aec3" async> </script>
</head>
```

#2. Initialize Jeapie

**3.1 Init with Jeapie Widget** 

Call `Jeapie.push(["init"])` from a javascript file that is included in every page. Add param `createButton` with value `true`. If you want to update default text on widget add param `tooltipText` with you custom value.
```javascript
var Jeapie = Jeapie || [];
Jeapie.push(["init", {"autoRegister":false, "createButton": true, "tooltipText": "YOUR CUSTOM TEXT"}]);
```
The interactive button will appear on your site. Click it to open a window in which you will be able to allow sending notifications.

![Autoregister for users](/img/widget_example.png)

**3.2 Init with your custom button.** 

Call `Jeapie.push(["init"])` from a javascript file that is included in every page. Create or use your button and update `YOUR_CUSTOM_BUTTON_ID` with your button id.

```javascript
var Jeapie = Jeapie || [];
Jeapie.push(["init", {"autoRegister":false}]);

window.onload = function() {
	//Replace YOUR_CUSTOM_BUTTON_ID with your button id
	document.getElementById("YOUR_CUSTOM_BUTTON_ID").onclick = registerPush;

	function registerPush() {
	    Jeapie.push(["registerHttp");
	}
}

```

**That's It!**

That’s it for now - the setup is complete. See our [Web SDK API](Website-SDK-API.md) for more functions and [our examples](https://github.com/jeapie/Jeapie-Website-SDK/tree/master/Examples) on our Github page.
