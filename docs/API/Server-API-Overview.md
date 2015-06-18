#Server API Overview

The Jeapie Server API serves purpose: Programmatically delivering notifications from your server or from one mobile device to another.


##Authentication

API requests are identified using [HTTP basic authentication](http://en.wikipedia.org/wiki/Basic_access_authentication).<br>
The username portion is the application key **"APP_KEY"**.<br>
The password portion is either the application secret **"APP_SECRET"**.


You can find API key of your mobile/web application here:
![Rest api key](/img/00000206.png)

**Code example**


```shell
// via shell
// example APP_KEY = 1e26f7bb3f81e1ab789d3e20b9cf6325
// example APP_SECRET = 9bb59fcbff38b85647c421c65cca06ce
curl -X \
    -u "1e26f7bb3f81e1ab789d3e20b9cf6325:9bb59fcbff38b85647c421c65cca06ce" \
    -H "Content-Type: application/json" \
    https://app.jeapie.com/api/v2/push.json

// or
curl -X \
    -u "1e26f7bb3f81e1ab789d3e20b9cf6325:9bb59fcbff38b85647c421c65cca06ce" \
    -H "Content-Type: application/json" \
    https://app.jeapie.com/api/v2/push.json
```
