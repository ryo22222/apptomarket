This shows an example of how to create an Activity using sdkBridger

# Code Example #

Here is a simple Activity class that uses sdkBridger

```

package com.example;


import com.google.devtools.simple.runtime.components.Component;
import com.google.devtools.simple.runtime.components.HandlesEventDispatching;
import com.google.devtools.simple.runtime.components.android.*;
import com.google.devtools.simple.runtime.events.EventDispatcher;


//A simple class that demonstrates how to create a Form (Android Activity) using sdkBridger.
public class ActivityExample extends Form implements HandlesEventDispatching {

//Initialize components
TextBox textBox;
Button btnSubmit;
Button btnCancel;
HorizontalArrangement horiz;

//This is basically the main method. This method will automatically be invoked when the onCreate is invoked
void $define() {
//Define a HorizontalArrangement that horizontally fills the screen
horiz = new HorizontalArrangement(this, LENGTH_FILL_PARENT);


//Add a text box in the Horizontal Arrangement
new Label(horiz, "Enter Name: ");
//Next to the above label, add a text box and set it to fill parent
textBox = new TextBox(horiz, "", LENGTH_FILL_PARENT);


//reuse the same HorizontalArrangement
//
horiz = new HorizontalArrangement(this, LENGTH_FILL_PARENT);


//Now in this layout, add 2 buttons as follows. The buttons will size accordingly to fill screen
btnSubmit = new Button(this, "Submit", LENGTH_FILL_PARENT);
btnCancel = new Button(this, "Cancel", LENGTH_FILL_PARENT);


//Register listener for Initialize and Click events. To know list of
//2nd argument can be anything
//3rd argument is the Event Name. An event name equates to App Inventor events. For example look at
//App Inventor ListPicker in the Blocks Editor; it has AfterPicking, BeforePicking, GotFocus, LostFocus
//However, ListPicker does not take in any arguments (note in AI, block does not have any sockets)
//Another example is Screen1. It has ErrorOccured event (check it in App Inventor). This event has
//arguments (4 sockets in AI)
EventDispatcher.registerEventForDelegation(this, "appName", "Initialize");
EventDispatcher.registerEventForDelegation(this, "appName", "ErrorOccured");
EventDispatcher.registerEventForDelegation(this, "appName", "Click");

}


//The dispatchEvent is used to trap the events
@Override
public boolean dispatchEvent(Component component, String id, String eventName, Object[] args) {

//if initialized event is triggered
if (component.equals(this) && eventName.equals("Initialize")) {
//call some a method to do initialization
initData();
return true;
}

else if (component.equals(this) && eventName.equals("ErrorOccured")) {
//In AI, check Screen1.ErrorOccured. Note that is has 4 sockets. Those equate to these arguments
handleError((String) args[0], (String) args[1], (Integer) args[2], (String) args[3]);
return true;
}

else if (eventName.equals("Click")) {
//We are now dealing with Click event.
if (component.equals(btnSubmit)) {
//Submit button was clicked

//TODO: Add logic here

return true;
}
else if (component.equals(btnCancel)) {
//Cancel button was clicked

//TODO: Add logic here

return true;
}
else {
//Some other button was clicked. Handle logic as needed

//Return false indicating that we did not process this event
return false;
}
}

//Add event checking here

return false;
}

private void initData() {
//Add some initialization logic here
}

private void handleError(String component, String functionName, int errorNumber, String message) {
//Add error processing logic here
}
}
```