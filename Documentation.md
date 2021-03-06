# Vidcoin Unity SDK - QuickStart Guide

![Vidcoin](https://documentation.vidcoin.com/images/Vidcoin-Logo.png)

Unity version: 1.6.9          
Packaged iOS SDK version: 1.4.5         
Packaged Android SDK version: 1.3.8         
Packaged tvOS SDK version: 1.0.1         
Manager: https://manager.vidcoin.com      
Contact: publishers@vidcoin.com     

## Overview						
Vidcoin Unity SDK enables you to broadcast videos in your apps in order to give users access to restricted content or to obtain virtual currency for free.
This document and the archive contain all the information you need in order to integrate our solution and start broadcasting videos. You can also contact us directly at publishers@vidcoin.com.

## Account Settings						
An approved and valid publisher account is necessary in order to use the SDK. If you do not have an account, please sign up directly on [https://manager.vidcoin.com](https://manager.vidcoin.com).
This also grants you access to statistics and detailed reports in our Publishers Back-Office.

### App Creation
You can access App Creation in the “App” menu of your publisher area. The creation of an app generates an “App ID” which will be mandatory in order to use the Vidcoin web SDK.

### Placement Creation			
A Placement represents the zone in your app where the videos will be available for broadcasting.

Basic configuration allows users to access a specific part of the app by watching a video. Once the advertisement's guaranteed duration is reached, you can unlock the content.		

If you want to reward your users with items or currency, you will have more settings available : 			
- Reward name: name of your virtual currency.		
- You can choose 2 types of rewards for the user:		
	- Conversion rate: rate defining how much 1€ equals of your virtual currency. Please note that we recommend that you use a low exchange rate such that 1€ = 1000 of your virtual currency. This will prevent any problems of crediting users with small amounts of virtual currency.
	- Fixed reward: amount of virtual currency the user will be rewarded for 1 view.
	- Callback URL (Optional): URL that will be used to validate the transaction on your servers.		

## Setting up the framework in your Unity Project

### Step 1 : Getting the Vidcoin Unity Package
Download and open the zip file from Github: [https://github.com/VidCoin/VidCoin-Unity-SDK](https://github.com/VidCoin/VidCoin-Unity-SDK)

### Step 2 : Importing Vidcoin into the Unity project
Open your project in Unity and select “Assets/Import Package/Custom Package...”.
Navigate to your download folder and select VidCoin.unitypackage. Click on the “All” button first, then click on the “Import” button.

![Image1](https://documentation.vidcoin.com/images/Vidcoin-Unity-1.png)

*Note : All files in the “Plugins” folder are required for the plugin to work. The “Sample” folder contains a simple scene to demonstrate the use of the plugin and can be omitted.*

#### Updating the plugin
If a new version of the Unity package is released, first download it on Github.
Then, simply import the package as described in Step 3. New files will be added while existing files will automatically be updated.

![Image2](https://documentation.vidcoin.com/images/Vidcoin-Unity-2.png)

### Step 3 : Set up Vidcoin in your app
To use Vidcoin in your app, follow these simple steps :
1. Open the first scene in your app
2. Add the Vidcoin prefab to the hierarchy
3. Fill in your Vidcoin AppID in the inspector.

![Image3](https://documentation.vidcoin.com/images/Vidcoin-Unity-3.png)

You can now use Vidcoin in your app. For more details on the usage, please keep reading this guide.

## Setting up Vidcoin for Android

Before you build your Unity project for Android, please follow these steps to make sure Vidcoin runs flawlessly.

### AndroidManifest.xml
Vidcoin requires additions to the default AndroidManifest.xml file generated by Unity.

#### If you use a custom AndroidManifest.xml
- Add the following lines right before the `</application>` tag:
```xml
<activity
    android:name="com.vidcoin.sdkandroid.extensions.MovieActivity"
    android:launchMode="singleTop"
    android:configChanges="orientation|screenSize"
    android:theme="@style/VC__AppTheme.NoActionBar.FullScreen" />
<activity
    android:name="com.vidcoin.sdkandroid.extensions.WebViewActivity"
    android:exported="false"
    android:parentActivityName="com.vidcoin.sdkandroid.extensions.MovieActivity"
    android:theme="@style/VC__AppTheme" >
    <meta-data
        android:name="android.support.PARENT_ACTIVITY"
        android:value="com.vidcoin.sdkandroid.extensions.MovieActivity" />
</activity>
<activity
    android:name="com.vidcoin.sdkandroid.extensions.FullScreenPlayerActivity"
    android:theme="@style/VC__AppTheme.NoActionBar.FullScreen" />
```

- Add the following permissions:
```xml
<uses-permission android:name="android.permission.INTERNET" />
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
```

- Add the following declaration of service:
```xml
<service
    android:name="com.vidcoin.sdkandroid.core.MediaDownloadService"
    android:exported="false" />
```

- Add the following declaration for Google Play Services:
```xml
<meta-data
    android:name="com.google.android.gms.version"
    android:value="7095000" />
```

**Optional: Add the WAKE\_LOCK permission to your manifest**
Vidcoin recommends you to use the WAKE\_LOCK permission to your AndroidManifest.xml, using the following line :
```xml
<uses-permission android:name="android.permission.WAKE\_LOCK"/>
```
The WAKE\_LOCK permission helps the screen to stay awake during the duration of the video. It is recommended to add this to your manifest to increase user-experience, therefore more views.

#### If you don't use a custom AndroidManifest.xml
The Vidcoin Unity package contains a modified AndroidManifest.xml located in the *Plugins/VidCoin* folder.
Open the AndroidManifest.xml file and replace the attribute on line 2 with your own package name:
```java
package = ”com.VidCoin.SDK”
```
Copy over the AndroidManifest.xml file to the *Assets/Plugins/Android* folder of your Unity Project.

### Deleting duplicate libraries
Vidcoin for Android uses 4 common libraries to function :
- android-support-v4.jar
- volley.jar
- gson-2.2.4.jar
- google-play-services-ads.jar

If one or more of these libraries already exist in your Unity project, please delete any duplicate to avoid errors during the build phase.

## Setting up Vidcoin for iOS or tvOS
When building your project for iOS or tvOS, Unity creates an Xcode project. You must follow these steps to use Vidcoin:
1. Open your Xcode project.
2. Click on your target and go to Build Phases:

![Image4](https://documentation.vidcoin.com/images/Vidcoin-Unity-4.png)

3. Under “Link Binary with Librairies”, click on the “+” button to add the following frameworks to the project :
    - AdSupport.framework (iOS and tvOS)
    - AVFoundation.framework (iOS and tvOS)
    - CoreMedia.framework (iOS and tvOS)
    - CoreTelephony.framework (iOS only)
    - SystemConfiguration.framework (iOS and tvOS)
    - WebKit.framework (iOS only, set to *Optional*)
    - StoreKit.framework (iOS only, set to *Optional*)
4. Drag and Drop the Vidcoin iOS or tvOS SDK (located in the *Assets/Plugins/iOS* or *Assets/Plugins/tvOS* folder of your Unity project) on your Xcode project and make sure “Copy items if needed” is ticked.
5. Under “Copy Bundle Resources”, click on the “+” button, then on the “Add Other…” button. Navigate to the *Assets/Plugins/iOS* or *Assets/Plugins/tvOS* folder of your Unity project and select VidCoin.bundle

![Image5](https://documentation.vidcoin.com/images/Vidcoin-Unity-5.png)

*Note : Make sure that “Copy items if needed” is ticked.*

You can now build your Xcode project as you normally would.

*Note : In Unity, if you select “Replace” when building your project for iOS or tvOS, you will have to repeat the full setup process. To avoid that, you should select “Append” when prompted.*

![Image6](https://documentation.vidcoin.com/images/Vidcoin-Unity-6.png)

### Recommended step: Configuring App Transport Security (ATS) Settings
With iOS 9, Apple introduced a new feature called App Transport Security (ATS), which requires your app to make secure network connections via SSL, and enforces HTTPS connections through its requirements on the SSL version, encryption cipher, and key length.      
Since v1.3.0, Vidcoin’s iOS SDK is fully compatible with iOS 9, which means you should not worry about any ad revenue drop from our service. Nevertheless, some of our partners will not be able to make the transition that easily. To ensure you get the best service possible from our product, we recommend you disable ATS in your project.

With iOS 9, Apple provided a way to easily disable ATS in a project, by add the following lines to the project’s `.plist` file:

```xml
<key>NSAppTransportSecurity</key>
<dict>
    <key>NSAllowsArbitraryLoads</key>
    <true/>
</dict>
```

With iOS 10, Apple is restricting the usage of `NSAllowsArbitraryLoads`, and setting this key’s value to YES triggers App Store review and requires justification.      
When building against iOS 10, you can disable ATS for web content only:

```xml
<key>NSAppTransportSecurity</key>
<dict>
    <key>NSAllowsArbitraryLoadsInWebContent</key>
    <true/>
</dict>
```

### Updating the iOS or tvOS framework
To update the iOS or tvOS framework in your Xcode project, simply remove the old versions of the .bundle and .framework from the project, and add the new bundle and framework files :
1. Open your Xcode project.
2. Click on your target and go to Build Phases
3. Under “Copy Bundle Resources”, select VidCoin.bundle and click on the “-” button
4. Under “Link Binary With Librairies”, select VidCoin.framework and click on the “-” button
5. Follow the setup process again

## How to use Vidcoin in your Unity Project
*Note : You can refer to the file VidCoinExample.cs included in VidCoin.unitypackage to see how you can use Vidcoin.*

### Setting up Vidcoin in the app
Follow step 3 to set up Vidcoin in your Unity app.
You can then use Vidcoin from any script in the app by calling:
```c
VidCoin.OneOfTheMethods();
```

### Update the user information
It’s really important that you send us as much information on your user as you can, so that we can target the ads appropriately. The easy way to do this is the following :
```c
// Update user informations to get better targeted ads
Dictionary<string,string> userInfos = new Dictionary<string, string>();
userInfos.Add (VidCoin.VCUserGameID,"UserName");
userInfos.Add (VidCoin.VCUserBirthYear,"1980");
userInfos.Add (VidCoin.VCUserGenderKey,VidCoin.VCUserGenderMale);
VidCoin.UpdateUserDictionary(userInfos);
```
*Note : To use the* `Dictionary<string,string>` *type, you have to import “System.Collections.Generic” in the script.*

You can pass any of these 3 key-value pairs, all keys and values being string objects.

| Key  | Values | Description |
| :-------------: | :-------------: | :-------------: |
| VCUserGameID | Any string object | This is the string you use to identify the user in your app. This will be used in case you implement a server callback. |
| VCUserBirthYear | Any string object like “1990” | The birth year of the user, in a string. |
| VCUserGenderKey | VCUserGenderMale or VCUserGenderFemale | A string to specify the user’s gender. Any other value will be ignored. |

### Check if a video is available				
You may want to know if a video is available for a given placement. For example, you shouldn’t display a button inviting the user to watch a video if there is none in cache. Calling the class method `VidCoin.VideoIsAvailableForPlacement(string placementCode)` is the way to go :
```c
if( VidCoin.VideoIsAvailableForPlacement("yourPlacementCode") ){
    Debug.Log ("Video(s) ready to be played.");  // OK
} else {
    Debug.Log ("No video available right now.");  // No video to play
}
```
This method will return a `bool`, equal to `true` if at least one video is ready to be played for the placement you passed as parameter, and `false` otherwise.

### Play a video					
You can present a video to the user by calling the following method :
```c
VidCoin.PlayAdForPlacementCode("yourPlacementCode",true);
```
You can choose wether you want the controller appearance to be animated or not by setting the second parameter to true or false. The animation is a sliding appearance of the player from the bottom of the screen.

If a video is ready to be played for this placement, the player will appear and the video will start.

### Manage events
There are four types of events that the framework triggers. Each event will call a list of functions when they are triggered. You can add as many functions to these lists as you’d like.

To add a function to one of the lists, simply call the following line:
```c
VidCoin.NameOfEvent.Add(NameOfMyFunction);
```
*Note : The prototype your function must have depends on the event you wish to add it to. See below for more information.*

#### Simple events
You can add functions to these events if they match the following prototype :
```c
public void NameOfMyFunction();
```

###### Event `OnCampaignsUpdate`
Triggered regularly, whenever a change happens in the framework : if the list of available videos changed, if a video is available, etc…

###### Event `OnViewWillAppear`
Triggered just before the video player appears on screen. *Note : It is recommended that you pause the app and the app’s audio on this event.*

#### Events with informations about the view
You can add functions to these events if they match the following prototype :
```c
public void NameOfMyFunction2(Dictionary<string,object> viewInfo);
````
*Note : To use the* `Dictionary<string,object>` *type, you have to import “System.Collections.Generic” in the script.*

###### Event `OnViewDidDisappear`
Triggered right after the video player left the screen. You can access basic information about the video that was just watched in the viewInfo dictionary. Here are the values you can access:		 	 	 	
  - `string status = (string) viewInfo["status"];`
  - `int reward = (int) viewInfo["reward"];`
  - `VidCoin.VCStatusCode statusCode = (VidCoin.VCStatusCode) viewInfo["statusCode"];`

The `reward` variable informs you on the amount the user will be rewarded when the view is validated on the server-side.

The `statusCode` variable can have three values:
  - `VCStatusCodeSuccess` : The video was watched correctly
  - `VCStatusCodeCancel`  : The user canceled the video
  - `VCStatusCodeError` : Something went wrong, and the user couldn’t watch the video

###### Event `OnDidValidateView`
Triggered when the server answers after the framework tried to validate the view. You can access basic information about the video that was just watched in the viewInfo dictionary. Here are the values you can access:
  - `string status = (string) viewInfo["status"];`
  - `int reward = (int) viewInfo["reward"];`
  - `VidCoin.VCStatusCode statusCode = (VidCoin.VCStatusCode) viewInfo["statusCode"];`

The value associated to the `reward` key now contains the amount of your in-app currency that was *actually* credited to the user on the server side.

The `statusCode` variable can have two values:
  - `VCStatusCodeSuccess` : The Vidcoin server validated the view
  - `VCStatusCodeError` : The Vidcoin server denied the view

A good place to add functions to the events’ lists is in the `Start()` function of scripts.
Do not do this in the `Awake()` function as the lists might not be initialized and it could cause errors.

*Note : This event will always be triggered after `OnViewDidDisappear`*

## Submitting to the App Store (iOS/tvOS Only)

When you submit your app for Apple’s approval, you will be asked if your app uses the Advertising Identifier. Vidcoin’s framework does use this identifier, in order to serve advertisements within your app:

![Image7](https://documentation.vidcoin.com/images/Vidcoin-Unity-7.png)

## Advice for integration
The integration of the Vidcoin solution must not deteriorate the user experience.
Because of certain parameters and restrictions (country, number of videos already viewed...) there may not always be available videos.

A non-blocking integration consists in offering Vidcoin to the user as an alternate solution to the classical running of the app.

Here is an example :
- The user is presented a given view of the app
- A button “Please sign-in to access your content” is presented
- Make the view subscribe to Vidcoin’s events, and implement the method triggered by the event called `OnCampaignsUpdate`
- In this method, if a call to Vidcoin’s method `VideoIsAvailableForPlacement` returns true for the given placement code, a second button can be presented: “Watch a video to access your content”
- If the call returns false, the second button should not be made visible.

This type of integration avoids proposing a user to watch a video if none is available, and does not damage the user experience. You should not expect videos to be always available.

The sample app gives a good example of a recommended integration.

## Server-side callback (optional)
If you want to use a server-side callback to credit your users, please refer to the following documentation: [http://documentation.vidcoin.com/Vidcoin-Server-Callback.html](http://documentation.vidcoin.com/Vidcoin-Server-Callback.html)
