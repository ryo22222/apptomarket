This shows an example of how to create a service using sdkBridger

# Code Example #

Here is a sample service example that uses sdkBridger

```

package com.mycompany.myapp;

import com.google.devtools.simple.runtime.components.Component;
import com.google.devtools.simple.runtime.components.HandlesEventDispatching;
import com.google.devtools.simple.runtime.components.android.BridgeService;
import com.google.devtools.simple.runtime.components.android.OrientationSensor;
import com.google.devtools.simple.runtime.components.android.Texting;
import com.google.devtools.simple.runtime.components.android.TinyDB;
import com.google.devtools.simple.runtime.events.EventDispatcher;


/*

* An example to show how to write a service using sdkBridger
*/
public class MyService extends BridgeService implements HandlesEventDispatching {

//Current Non-Visual components that can be used in service
//No visual components in service
TinyDB tinyDB;
Texting texting;
OrientationSensor orientationSensor;  //Not used in this sample
LocationSensor locationSensor;        //Not used in this sample

//This is basically the main method.
//This method will automatically be invoked when the onCreate is invoked
void $define() {

tinyDB = new TinyDB(this);
texting = new Texting(this);
texting.ReceivingEnabled(true);
orientationSensor = new OrientationSensor(this);

//Register listeners for Initialize and MessageReceived events.
//2nd argument can be anything
//3rd argument is the Event Name. An event name equates to App Inventor events. For example look at
//App Inventor Texting in the Blocks Editor
//or HERE: http://beta.appinventor.mit.edu/learn/reference/components/social.html#Texting
//For MessageReceived event it has 2 arguments, (sockets in AI Block Editor) as follows:
// argument 1: number
// argument 2: messageText
EventDispatcher.registerEventForDelegation(this, "MyService", "Initialize");
EventDispatcher.registerEventForDelegation(this, "MyService", "MessageReceived");
}

@Override
public boolean dispatchEvent(Component component, String id, String eventName, Object[] args) {
if (component.equals(this))
{
if (eventName.equals("Initialize"))
{
initData();
return true;
}
else if (eventName.equals("MessageReceived"))
{
//texting message was received
//See below to know what arguments should be used:
// http://beta.appinventor.mit.edu/learn/reference/components/social.html#Texting
processReceivedMessage((String) args[0], (String) args[1]);
return true;
}
}

//Return false because we didn't have an event handler
return false;
}

/**
* This method will get invoked when service is started
*/
private void initData()
{
//TODO: add initialization logic here
}

private void processReceivedMessage(String fromNumber, String message)
{
//TODO: add logic here

//Sample code. Store into our TinyDB
tinyDB.StoreValue("TAG_PHONE_NUMBER", fromNumber);
tinyDB.StoreValue("TAG_RECEIVED_MESSAGE", message);

//Send some response back
texting.PhoneNumber(fromNumber);
texting.Message("Received your message of: " + message);
texting.SendMessage();


//TODO: add code as needed

}
}