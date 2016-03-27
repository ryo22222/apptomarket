# AndroidManifest #

Every application must have an AndroidManifest.xml file (with precisely that name) in its root directory. The manifest presents essential information about the application to the Android system, information the system must have before it can run any of the application's code. For detailed info, please see here: http://developer.android.com/guide/topics/manifest/manifest-intro.html


# Code Example #

Below is a simple example of an Android Manifest file. Please note that the activities for ListPicker and WebView have specifically been added to work when using sdkBridger -- see sdkBridgerIntro

```

<?xml version="1.0" encoding="utf-8"?>
<manifest xmlns:android="http://schemas.android.com/apk/res/android"
package="com.examples"
android:versionCode="1"
android:versionName="1.0">
<uses-sdk android:minSdkVersion="5" />

<application android:icon="@drawable/icon" android:label="@string/app_name">
<activity android:name=".MyActivity"
android:label="@string/app_name" android:screenOrientation="portrait">
<intent-filter>

<action android:name="android.intent.action.MAIN" />
<category android:name="android.intent.category.LAUNCHER" />


Unknown end tag for &lt;/intent-filter&gt;





Unknown end tag for &lt;/activity&gt;




<!-- Activity needed for ListPicker -->
<activity android:name="com.google.devtools.simple.runtime.components.android.ListPickerActivity"
android:screenOrientation="behind"
android:configChanges="keyboardHidden|orientation">


Unknown end tag for &lt;/activity&gt;




<!-- Activity needed for WebView -->
<activity android:name="com.google.devtools.simple.runtime.components.android.WebViewActivity"
android:screenOrientation="behind"
android:configChanges="keyboardHidden|orientation" >


Unknown end tag for &lt;/activity&gt;





Unknown end tag for &lt;/application&gt;




Unknown end tag for &lt;/manifest&gt;




```