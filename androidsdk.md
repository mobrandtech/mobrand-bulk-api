This document shows the process of integrating the Mobrand SDK with your Android application. If you have any questions, please email us at [support@mobrand.com](mailto:support@mobrand.com).

Here are the basic integration steps:

1. Download the files from our repository (optional)
2. Add our SDK as a dependency to your project.
3. Put the code where you want to open ad units in your app.

# 1. Download the Mobrand Android SDK


The mobrand SDK is available as an Android Archive via our maven repository. To add the mobrand-sdk dependency, open your project's `build.gradle` and update the `repositories` and `dependencies` blocks as follows:  

```groovy
    repositories {
        // ... other project repositories
        jcenter() // or mavenCentral()
        maven { url 'http://maven.mobrand.net/maven2' }
    }


    android {
        //your config

        //...

        packagingOptions {
            exclude 'META-INF/LICENSE'
            exclude 'META-INF/NOTICE'
        }
    }

    // ...

    dependencies {
      // ... other project dependencies

        // adds our default Appwall adunit to your project
        compile('com.mobrand.sdk:appwall-classic:1.0.5')

        // adds the SimplyRed Interstitial to your project
        compile('com.mobrand.sdk:simplyred:1.0.0')

    }
```

# 2. Updating your Android Manifest

Your AndroidManifest.xml will need to be updated in order to complete the SDK integration. Add the following permissions and activity declarations according to the bundle you are integrating.

### Default Bundle:

  Declare the following permissions:

  ```xml
  <uses-permission android:name="android.permission.INTERNET" />
  <uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
  <uses-permission android:name="android.permission.READ_PHONE_STATE"/>
  ```

  **Note:** `READ_PHONE_STATE` or `ACCESS_NETWORK_STATE` are required so the SDK can retrieve relevant information from your users. We do not store this information, its for ads tracking purposes only.

  Declare the following activities:

  ```xml
  // add our default AppWall
  <activity android:name="com.mobrand.appwall.classic.AppWall"/>

  // add our SimplyRed Interstitial
  <activity android:name="com.mobrand.simplyred.MobrandSimplyRedInterstitial" />


  //more AdUnits to come!
  ```

  Add this tag to your `<application>` so the SDK can identify your app:
  ```xml
  <meta-data android:name="mobrand_appid" android:value="YOURAPP_ID" />
  ```

The appid can be retrieved from your backoffice going to:

1. My Apps
2. Click the app that you are integrating
3. Your ID will be at to the top

![appid](https://github.com/mobrandtech/mobrand-sdk-android/wiki/images/appid.png)


# 3. Displaying Ads

![adunits](https://github.com/mobrandtech/mobrand-sdk-android/wiki/images/githubadunits.png)

In this section, we describe how you can display ads.

## Sample code

Checkout [[Mobrand Sample App|https://github.com/mobrandtech/mobrand-sdk-android/tree/master/app]] for a working example.

## Load our Default AdUnits

All you have to do is run this in any activity or fragment.

```java

import com.mobrand.sdk.AppWall;

public void onClickAppWall(Context context, String placementId){
    AppWall.start(context, placementId);
}

public void onClickInterstitial(Context context, String placementId){
    MobrandSimplyRedInterstitial.start(context, placementId);
}

// more AdUnits to come!

```

An AdUnit needs a `placementId` so you can measure the different traffic from each AdUnit. The ID that you define in your code will be automatically generated in the backoffice.



# 4. Using ProGuard

```
-keep class com.mobrand.sdk.** {*;}
-keepclassmembers class ** {
    public void onEvent*(***);
}
```