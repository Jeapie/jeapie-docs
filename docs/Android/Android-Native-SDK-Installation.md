#Android Native SDK Installation

**'Google Play services' & 'Android Support Library'**

Jeapie requires Google Play services (google-play-services_lib) and Android Support Library v4 (android-support-v4.jar). android-support-v13.jar can be used instead if your project already requires it.

**1.** Download the latest [Jeapie Android SDK](https://github.com/Jeapie/jeapie-android).

**2.** Copy \*.aar file into the lib folder of your android project.


**3.** Set `sdk filename` of the \*.aar file and `play-services` in gradle.

```gradle
dependencies {
    compile(name:'jeapie-sdk-x.x.x', ext:'aar')
    compile 'com.google.android.gms:play-services:6.5.87'
    compile fileTree(dir: 'libs', include: ['*.jar'])
    compile 'com.android.support:appcompat-v7:22.0.0'
}

repositories{
    flatDir{
        dirs 'libs'
    }
}
```

**4.** Paste permissions into the `Manifest` file of your Android project .

Replace `{APP_PACKAGE}` by your own package.

```xml
    <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE"/>
    <uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE"/>
    <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE"/>
    <uses-permission android:name="android.permission.INTERNET"/>
    <uses-permission android:name="android.permission.GET_ACCOUNTS"/>
    <uses-permission android:name="android.permission.WAKE_LOCK"/>
    <uses-permission android:name="com.google.android.c2dm.permission.RECEIVE"/>
    <uses-permission android:name="android.permission.READ_PHONE_STATE"/>
    <uses-permission android:name="android.permission.VIBRATE"/>
    <uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION"/>
    <uses-permission android:name="android.permission.ACCESS_FINE_LOCATION"/>
    <uses-permission android:name="com.google.android.providers.gsf.permission.READ_GSERVICES"/>
    
    <permission
            android:name="{APP_PACKAGE}.permission.C2D_MESSAGE"
            android:protectionLevel="signature"/>
    
    <uses-permission android:name="{APP_PACKAGE}.permission.C2D_MESSAGE"/>
    
```

**5.** Paste configs into the `Manifest` file of your Anroid project. 

Replace `{APP_SECRET}` and `{APP_KEY}` by your own keys from Jeapie dashboard.
![Rest api keys](/img/00000206.png)


Also replace  `A{PROJECT_ID}` by a project number from your Google Console.<br>
Look [How to get project number](Android-Generating-a-GCM-Push-Notification-Key/#step-1-create-a-google-project-and-save-the-project-number)

<div class="admonition note">
<p class="first admonition-title"><span class="highlighted">Note</span></p>
<p class="last">{PROJECT_NUMBER} value is a number but make sure you prefix it with the letter <b>“A”</b> as in the example above.
Example: "A1111111111"</p>
</div>


```xml
<application ....>
        <meta-data
            android:name="com.jeapie.key"
            android:value="{APP_KEY}"/>

        <meta-data
            android:name="com.jeapie.secret"
            android:value="{APP_SECRET}"/>

        <meta-data
            android:name="project_number"
            android:value="A{PROJECT_NUMBER}"/>


        <receiver android:name="com.jeapieLib.reciever.GCMReceiver">
            <intent-filter>
                <action android:name="com.google.android.c2dm.intent.RECEIVE"/>
                <action android:name="com.google.android.c2dm.intent.REGISTRATION"/>
                <category android:name="com.jeapieApp"/>
            </intent-filter>
        </receiver>

        <receiver android:name="com.jeapieLib.GCMReceiver">
            <intent-filter>
                <action android:name="com.google.android.c2dm.intent.RECEIVE"/>
                <action android:name="com.google.android.c2dm.intent.REGISTRATION"/>
                <category android:name="com.jeapieApp"/>
            </intent-filter>
        </receiver>

        <receiver android:name="com.jeapieLib.InternetConnectionReceiver"
                  android:exported="false">
            <intent-filter>
                <action android:name="android.net.conn.CONNECTIVITY_CHANGE"/>
            </intent-filter>
        </receiver>

        <service android:name="com.jeapieLib.service.EventsSenderService"
                 android:exported="false"/>

        <service android:name="com.jeapieLib.service.LocationTrackingService"
                 android:exported="false"/>

</application>
```

**6.** Paste the code into "Launch Activity"

```java
JeapieAPI.init(getApplicationContext());


//tracking push opening
Bundle bundle = getIntent().getExtras();
JeapieAPI.getInstance().trackPushOpen(bundle);
```


**7.** Now you can use jeapie sdk methods

<!--* To see all available methods, see our [Android SDK API Documentation](Android-Native-SDK-API.md).-->
