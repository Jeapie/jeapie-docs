# api/v2/push.json Send Push Notification via API

#### Endpoint

`https://go.jeapie.com/api/v2/push.json`

#### Method

`Post`

#### Authentication

Click the following link to read about [Jeapie authentication](Server-API-Overview/#authentication).

#### Full example for Mobile platforms

```json
    {
        // This params are cross-platform for all platforms
        "send_date":"now", // or UNIX_TIME. Optional
        "message": "push text",   // Required
        "data":{"key": "value"}, // Optional
        "platforms": ["android", "ios"], // Optional
        "badge": "inc", or number [0-999] // Optional
        "default_sound": 1, // Optional
        "ttl": 3600, // Optional

        // Android additional settings. Optional
        "android": {
            "sound" : "soundfile",
            "header":"header",
            "icon": "icon",
            "custom_icon": "http://example.com/image.png",
            "banner": "http://example.com/banner.png"
        },
        
        // iOS (production mode). Optional
        "ios": {
            "badge": 5,
            "sound": "file.wav", // or "default"
            "category_id": "1", // iOS new feature
            "content-available": 1
        },
        
        // iOS (development mode). Optional
        "ios_dev": {
            "badge": 5,
            "sound": "file.wav", // or "default"
            "category_id": "1", // iOS new feature
            "content-available": 1
        },

        // Send to all devices
        "audience": {
            "all": 1 // send to all devices
        }
    }
```

#### Full example for Web platforms

```json
{
        // This params are cross-platform for all platforms
        "send_date":"now", // or UNIX_TIME. Optional
        "message": "push text",  // Required
        "platforms": ["chrome", "safari"], // Optional
        "ttl": 3600, // Optional

        // Safari related (in development). Optional
        "safari": { 
            "header": "Title",
            "redirect_url": "http://example.com"
        },

        // Chrome related (in development). Optional
        "chrome": {
            "header": "title example",
            "icon": "http://example.com/icon.png",
            "redirect_url": "/example.html" // Default
        },


        // you should use only one of this params
        "audience": {
            "all": 1 // send to all devices
        }
    }
```
### Description of the params
##### Cross-platform params
|           |                                |
|----------:|:-------------------------------|
| **send_date** *Optional* | **Mixed**: String or Int <br> *default:* `"now"` |
| | Time for scheduled push. Can be "now" or UNIX_TIME <br> Example: <br> `"send_date": "now"` or `"send_date": 1430568855` |
| **message** `Required` | **String** <br> *Required unless content_available=true* |
|| Push text. Example: <br> `"message": "hello, world"` |
| **data** *Optional* | **Hash** |
| | Extra data for push. Can contain additional data for for processing within the application. Example: <br> `"data": {"page": 1, "url": "http://example.com}"` |
| **badge** *Optional* | **Mixed**: String or Int |
| | Only for iphone and windows phone. For setting badge number use int, for incrementing badge number use "inc". Example: <br> `"badge": 3` or `"badge": "inc"` |
| **platforms** *Optional* | **Array** <br> List of mobile platforms: "android" <br> List of web platforms: "chrome", "safari" |
| | List of platforms. Example: <br> if mobile platforms: `"platforms": ["android", "ios"]` <br> or if web platforms: `"platforms": ["chrome", "safari"]` | 
| **default_sound** *Optional* | **Int**: `0` or `1` <br> *default:* `0` |
| | If you need default sound set `1` else `0`. Example: <br> `"default_sound": 1` |
| **ttl** *Optional* | **Int** <br> *default:* `3600` |
| | "Time to live" parameter - the maximum lifespan of a message in seconds. <br>Example: `"ttl":3600` |

##### Android params *(All params are optional)*

|           |                                |
|----------:|:-------------------------------|
| **sound** *Optional* | **String** |
| | Sound file name in the "res/raw" folder, do not include the extension. <br> Example: `"sound": "taff"` |
| **header** *Optional* | **String** |
| | Android notification header. <br>Example: `"header": "Header text"` |
| **icon** *Optional* | **String** |
| | Icon file name in the "res/drawable" folder. <br>Example: `"icon":"icon.png"` |
| **custom_icon** *Optional* | **String** |
| | Full path to icon file (http url) <br>Example: `"custom_icon": "http://example.com/icon.png"` |
| **banner** *Optional* | **String** |
| | Full path to banner file (http url) <br>Example: `"banner": "http://example.com/banner.png"` |

##### Chrome params *(All params are optional)*
|           |                                |
|----------:|:-------------------------------|
| **header** *Optional* | **String** |
| | Chrome notification header. <br>Example: `"header": "Header text"` |
| **icon** *Optional* | **String** |
| | Full path to icon file (http url <br>Example: `"icon": "http://example.com/icon.png"` |
| **redirect_url** *Optional* | **String** |
| | The relative url which is opened after clicking on a push. <br>Example: `"redirect_url": "/example.html"` |

##### iOS params *(All params are optional)*
|           |                                |
|----------:|:-------------------------------|
| **badge** *Optional* | **int** |
| |  Optional, integer. iOS application badge number. Example: `"badge": 1` |
| **sound** *Optional* | **String** |
| | Optional. Sound file name in the main bundle of application <br>Example: `"sound": "bingbong.aiff"` |
| **category_id** *Optional* | **int** |
| | Provide this key with a string value that represents the identifier property of the UIMutableUserNotificationCategory object you created to define custom actions. To learn more about using custom actions, see Using Notification Actions in iOS. |
| **content-available** *Optional* | **int** |
| | Provide this key with a value of 1 to indicate that new content is available. Including this key and value means that when your app is launched in the background or resumed, application:didReceiveRemoteNotification:fetchCompletionHandler: is called. |


##### iOS_DEV params *(All params are optional)*
|           |                                |
|----------:|:-------------------------------|
| **badge** *Optional* | **int** |
| |  Optional, integer. iOS application badge number. Example: `"badge": 1` |
| **sound** *Optional* | **String** |
| | Optional. Sound file name in the main bundle of application <br>Example: `"sound": "bingbong.aiff"` |
| **category_id** *Optional* | **int** |
| | Provide this key with a string value that represents the identifier property of the UIMutableUserNotificationCategory object you created to define custom actions. To learn more about using custom actions, see Using Notification Actions in iOS. |
| **content-available** *Optional* | **int** |
| | Provide this key with a value of 1 to indicate that new content is available. Including this key and value means that when your app is launched in the background or resumed, application:didReceiveRemoteNotification:fetchCompletionHandler: is called. |

##### Safari params *(All params are optional)*
|           |                                |
|----------:|:-------------------------------|
| **header** *Optional* | **String** |
| | Safari notification header (title). <br>Example: `"header": "Header text"` |
| **redirect_url** *Optional* | **String** |
| | The absolute url which is opened after clicking on a push. <br>Example: `"redirect_url": "http://example.com"` |

##### Audience *(Required)*
|           |                                |
|----------:|:-------------------------------|
| **all** | **Int** |
| | send to all devices. <br> Example: `"all": 1` |
| **tokens** | **Array<String>** |
| | Send to array of device (browser) tokens. Limit is 100 tokens. Example: <br> `"tokens": ["dec301908b9ba...8df85e57a58e40f96f", "523f4c2068674f1fe...2ba25cdc250a2a41"]` |
| **aliases** | **Array<String>** |
| | Array of device aliases set by sdk in mobile app or on web. Example: <br> `"aliases": ["own_id_device_1", "own_id_device_2", "own_id_device_3"]` |
| **tags** | **Array<String>** |
| | Array of tags set by sdk in mobile app or on web. Example: <br> `"tags": ["tag1", "tag2", "tag3"]` |


###Result Format
* [200 OK]()
```JSON
{
    "id":"55704a589e31ab441e8b4569",
    "status":"completed",
    "message":"test",
    "extra_data":[],
    "platforms":"Android",
    "badge":"inc",
    "default_sound":"1",
    "ttl":3600
}
```



##Shell Code Examples

Send push to all platforms and all devices immediately:

```Shell
curl -X POST \
     -H "Content-Type: application/json" \
     -u "APP_KEY:APP_SECRET" \
     --data '{
        "message": "test",
        "audience": {
            "all": 1
        }
     }' \
     https://go.jeapie.com/api/v2/push.json
```

Send push only to android devices with aliases setted in mobile app:

```Shell
curl -X POST \
     -H "Content-Type: application/json" \
     -u "APP_KEY:APP_SECRET" \
     --data '{
        "message": "test",
        "platforms": ["android"],
        "android": {
            "header": "title"
        },
        "audience": {
            "aliases": ["some_id1", "some_id2", "email@example.com"]
        }
     }' \
     https://go.jeapie.com/api/v2/push.json
```


Send push to Chrome and redirect to page after clicking on push

```Shell
curl -X POST \
     -H "Content-Type: application/json" \
     -u "APP_KEY:APP_SECRET" \
     --data '{
        "message": "Push message",
        "platforms": ["chrome"],
        "chrome": {
            "header": "title message",
            "icon": "http://example.com/icon.png",
            "redirect_url": "/relative_url.html"
        },
        "audience": {
            "all": 1
        }
     }' \
     https://go.jeapie.com/api/v2/push.json
```


```php
// auth
$APP_KEY    = '{paste_app_key_from_dashboard}';
$APP_SECRET = '{paste_app_secret_from_dashboard}';

//data
$pushData = [
    'message' => 'Push message',
    'chrome' => [
        'header' => 'push title',
        'icon' => 'http://example.com/icon.png',
        'redirect_url' => 'http://example.com',
    ],
    'audience' => [
        'all' => 1,
    ],
];

$pushDataString = json_encode($pushData);                                                                                
          
// post json request                                                                                                     
$ch = curl_init('https://go.jeapie.com/api/v2/push.json'); 
curl_setopt($ch, CURLOPT_USERPWD, $APP_KEY . ':' . $APP_SECRET);
curl_setopt($ch, CURLOPT_CUSTOMREQUEST, 'POST');                                                                     
curl_setopt($ch, CURLOPT_POSTFIELDS, $pushDataString);                                                                  
curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);    
curl_setopt($ch, CURLOPT_CONNECTTIMEOUT, 5); 
curl_setopt($ch, CURLOPT_TIMEOUT, 5);                                                                  
curl_setopt($ch, CURLOPT_HTTPHEADER, [                                                                          
    'Content-Type: application/json',                                                                                
    'Content-Length: ' . strlen($pushDataString)
]);                                                                                                                   
                                                                                                                     
$result = curl_exec($ch);
```
