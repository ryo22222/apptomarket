# Introduction #

sdkBridger is a super-set of original App Inventor Bridge that simplifies developing Android applications. sdkBridger lets you incorporate App Inventor components into apps that you create in Java with the standard Android SDK tools.


# Details #

sdkBridger is a set of library based on original App Inventor Bridge that simplifies development of Android applications. The library includes many visual and non-visual components for building apps. Refer to BridgeActivity for an example of how to create an Activity using sdkBridger. For example, below shows the full code that is required to create a Hello World! app:
```

package com.example3;

import com.google.devtools.simple.runtime.components.android.Form;
import com.google.devtools.simple.runtime.components.android.Label;

public class HelloWorldActivity extends Form {
void $define() {
new Label(this,"Hello World!");
}
}
```

# Using sdkBridger #
  1. Make sure you have installed Android SDK: http://developer.android.com/sdk/installing.html
  1. Download latest version of sdkBridger jar file from Downloads section (you can download the nightly version that includes features / updates that will be rolled into next version)
  1. Use your favorite Java IDE, create a project and set up library path pointing to sdkBridger jar file
  1. For API doc see http://3nportal.com/AIBridge/API

_**NOTE:**The latest changes will go into a nightly build called sdkBridgerNightly.jar. The nightly includes updates / enhancements based on latest sdkBridger version. You can also download and use this version also. See related sdkBridgerNightly wiki which contain information on updates to this version._