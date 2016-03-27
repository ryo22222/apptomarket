# Bridge Example - How to switch between screens #

An example to demos how to switch between screens using sdkBridger and how it differs with using Android SDK

## Using sdkBridger ##
When your app has multiple screens (activities), using sdkBridger, you can switch between screens as shown below.

_**NOTE 1:**_ You must declare all your activities in androidmanifest.xml

_**NOTE 2:**_ All your activities must exist in the same package

```

//switch to another activity without passing any parameters
startNewForm("MyOtherActivity");

//switch to another activity when you want to pass parameter
startNewForm("MyOtherActivity", "someParam");
```

## Using Android SDK ##
Code below shows how to use Android SDK to switch between screens:

```

//Switch to another activity without passing any parameter
Intent intent = new Intent(this, MyOtherActivity.class);
intent.putExtra("VALUE1", "value for MyOtherActivity");
intent.putExtra("VALUE2", "value for MyOtherActivity");

//Launches the activity for which you would like a result when it finished.
//When this activity exits, your onActivityResult() method will be called with the given REQUEST_CODE.

startActivityForResult(intent, REQUEST_CODE);

```