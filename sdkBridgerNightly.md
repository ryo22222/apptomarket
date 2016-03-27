# Introduction #

This page includes updates / enhancements to sdkBridger based on latest sdkBridger version, currently v1.0.1. Some time in future, the nightly will be released as an official version.

To download this nightly, use Downloads link or here: http://code.google.com/p/apptomarket/downloads/detail?name=sdkBridgerNightly.jar

# Details #

### 1. Sorting PickList ###
YailList (basically an ArrayList) can now be created in unsorted or sorted order. This is useful when you when you want to display sorted items in a ListPicker; e.g.
```

//create a string array for test purpose
String[] items = new String[]{"b", "c", "a"};

// create un-sorted list
YailList yailListUnsorted= YailList.makeList(items);

// create sorted list
YailList yailListSorted= YailList.makeList(items, true);

//now, add the items to a ListPicker, and display the sorted items
myListPicker.Elements(yailListSorted);
myListPicker.open();

//For debug purpose, display sun-sorted, sorted results in notifier
notifier.ShowMessageDialog("Unsorted\n" + yailListUnsorted + "\n\nSorted\n" + yailListSorted,
"unsorted vs sorted",
"Okay");
```

### 2. Keep Screen On ###
You can now control the screen to stay ON or OFF for your app
. Usage example is when you develop GPS / Navigation apps and you want to avoid screen from turning off.
```

//keep screen on while this application is running
setKeepScreenOn(true);
```

### 3. RadioButton and CheckBox ListPickers ###
Now, you can create a list that includes Checkboxes OR Radiobuttons. Setup and initialization is pretty much like usual ListPicker. See code below to see example. Here ListPickerCbRbActivity is the code and Here is how listpickers look like: <br><img src='http://www.3nportal.com/wikiImages/listPicker.jpg' />

<h3>4. Visual Component Alignment</h3>
Added simple methods for component alignment; e.g.:<br>
<pre><code><br>
Button aButton = new Button(this,"I'm Centered");<br>
aButton.Position(POSITION_CENTER_HORIZONTAL);<br>
<br>
Label aLabel = new Label(this,"I'm right aligned");<br>
aLabel.Position(POSITION_RIGHT);<br>
</code></pre>

<h3>5. Splash Screen</h3>
Added Splash class. The Splash can be used to create animated Splash screen that after n number of seconds, invokes your main Form (Activity). Can also be used when you want to terminate an app; e.g. Splash will display for 5 second then app will be closed.<br>
<pre><code><br>
package com.example3;<br>
<br>
import com.google.devtools.simple.runtime.components.android.util.Splash;<br>
<br>
public class MySplasher extends Splash {<br>
<br>
@Override()<br>
public void setupAndRun() {<br>
<br>
//this means just terminate app after splash<br>
activityToStart = null;<br>
<br>
//Use following to switch to a new activity<br>
//NOTE: Make sure you add your activity into androidmanifest.xml<br>
//&lt;activity android:name=".ListPickerCbRbActivity" android:label="@string/app_name" /&gt;<br>
// activityToStart = "ListPickerCbRbActivity";<br>
line1Msg ="Thanks";<br>
line2Msg ="For";<br>
line3Msg ="Using";<br>
line4Msg ="my App2";<br>
line5Msg ="Hope You Enjoy";<br>
pauseInSeconds=9;<br>
<br>
}<br>
<br>
}</code></pre>