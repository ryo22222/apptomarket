# Bridge Example - Using Canvas #

This example shows how to use canvas and set such properties as its height and width. For a more detailed bridge activity, please see BridgeActivity.

# Code Example #

Here is a simple Activity class that uses sdkBridger. This example shows how you can initialize Canvas and set such properties as its height and width

```

//TODO: Add package
//TODO: Add your imports

public class CanvasActivity extends Form implements HandlesEventDispatching {
//TODO: add components as needed

Canvas canvas;
ImageSprite imageSprite;

void $define()
{
//TODO: init components

canvas = new Canvas(this);
imageSprite = new ImageSprite(canvas);

//TODO: other compoents

//register events. Initialize is invoked when app is started OR when phone orientatin is changed
EventDispatcher.registerEventForDelegation(this, "appName", "Initialize");

}

//method for trapping events
@Override
public boolean dispatchEvent(Component component, String id, String eventName, Object[] args)
{
//Event handling
if (component.equals(this) && eventName.equals("Initialize"))
{
initData();
return true;
}
//TODO: More event handling

return false;
}


//Method called from our event handling processor. This is the place
//you can set properties such as height / width
private void initData()
{
//set the canvas size to be same as screen size
canvas.Height(this.Height());
canvas.Width(this.Width());
canvas.BackgroundImage("someImage.jpg");

imageSprite.Picture("glow1.png");
imageSprite.X(this.Width()/2);
imageSprite.Y(this.Height() - imageSprite.Height() - 20);

imageSprite.Speed(2);
//IMPORTANT: You HAVE TO invoke initialize method
imageSprite.Initialize();
imageSprite.Interval(32);
imageSprite.Enabled(true);

}

//TODO:
}

```