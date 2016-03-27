# Introduction #

This shows you how to create a Splash Screen using sdkBridger.

# Details #

Splash Screens are used to show an app introduction page that appears for a few seconds, while app is loading. After splash screen times-out, then the main screen (activity) of the app should be started.

Creating splash screen in sdkBridger is very simple. Here is the code to create a splash screen with default configuration:
```

package com.example3;
import com.google.devtools.simple.runtime.components.android.util.Splash;
public class MySplasher extends Splash {
@Override()
public void setupAndRun() {
//Change default configuration data in this method.

//Display splash for 5 seconds and then start MyMainActivity screen after 5 seconds
activityToStart = "MyMainActivity";

// pauseInSeconds=5;
// line1Msg ="Thanks";
// line2Msg ="For";
// line3Msg ="Using";
// line4Msg ="my App";
// line5Msg ="Hope You Enjoy";
}
}
```

That's all that was needed to create a splash screen that would appear for 5 second, animate the default (commented out messages) and then invoke your main activity (e.g. MyMainActivity). Please note that you MUST declare your activity in the androidmanifest.xml like below:
```

<activity android:name=".MyMainActivity" android:label="@string/app_name" />
```

The following are the **_current_** configuration data that can be changed:
```

//name of the activity to start after splash ends.
//If set to null, then app just terminates; useful when you want to end your app
// Please note that your activity has to be declared in androidmanifest.xml
activityToStart = "SomeActivityName"

pauseInSeconds=5;        //number of seconds to show splash screen

// Following are defaults to display, change as you need
line1Msg ="Thanks";
line2Msg ="For";
line3Msg ="Using";
line4Msg ="my App";
line5Msg ="Hope You Enjoy";
```