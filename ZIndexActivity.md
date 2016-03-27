# sdkBridger Example - Using Z Index #
This example shows how to use Z Index to set order of components.
A component with greater order is always in front of another component
with lower order.

# Code Example #

In this example, we set up a Canvas with 3 balls.
We use the Z Index to set their ordering preferences.

```

package com.example;

import com.google.devtools.simple.runtime.components.Component;
import com.google.devtools.simple.runtime.components.HandlesEventDispatching;
import com.google.devtools.simple.runtime.components.android.*;
import com.google.devtools.simple.runtime.events.EventDispatcher;


public class ZIndexActivity extends Form implements HandlesEventDispatching {
Canvas canvas;
Ball ball;
Ball ball2;
Ball ball3;

void $define() {
canvas = new Canvas(this);
ball = new Ball(canvas);
ball2 = new Ball(canvas);
ball3 = new Ball(canvas);

EventDispatcher.registerEventForDelegation(this, "test", "Initialize");
EventDispatcher.registerEventForDelegation(this, "test", "EdgeReached");
}


@Override
public boolean dispatchEvent(Component component, String id, String eventName, Object[] args) {
if (component.equals(this) && eventName.equals("Initialize")) {
initData();
return true;
}
else if (eventName.equals("EdgeReached")) {
//Hits edges of screen
if (component.equals(ball)) {
ball.Bounce((Integer) args[0]);
ball.Heading(ball.Heading() - 22);
return true;
}
else if (component.equals(ball2)) {
ball2.Bounce((Integer) args[0]);
ball2.Heading(ball2.Heading() - 27);
return true;
}
else if (component.equals(ball3)) {
ball3.Bounce((Integer) args[0]);
ball3.Heading(ball3.Heading() - 32);
return true;
}
}

return false;
}


/**
* Method called on startup to do caching, initialization. We need to do this so that
* AI initializes all sounds, otherwise, it will run into issue switching between sounds.
*/
private void initData() {
canvas.Height(this.Height());
canvas.Width(this.Width());
canvas.BackgroundImage("bg.jpg");

canvas.PaintColor(COLOR_BLUE);
canvas.FontSize(10f);

ball.Radius(24);
ball.PaintColor(COLOR_BLUE);
ball.Speed(12);
ball.Initialize();
ball.Interval(32);
ball.Enabled(true);
ball.X(50);
ball.Y(50);

ball2.Radius(34);
ball2.PaintColor(COLOR_RED);
ball2.Speed(12);
ball2.Initialize();
ball2.Interval(32);
ball2.Enabled(true);
ball2.X(100);
ball2.Y(100);

ball3.Radius(44);
ball3.PaintColor(COLOR_GREEN);
ball3.Speed(12);
ball3.Initialize();
ball3.Interval(32);
ball3.Enabled(true);
ball3.X(111);
ball3.Y(111);

//z-index is a property that is used to set the  order of components.
//A component with greater order is always in front of another component with lower order.
ball.Z(10);
ball2.Z(20);
ball3.Z(30);
}

}

```