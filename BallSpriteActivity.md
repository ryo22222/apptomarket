# Bridge Example - Shows how to use CollidedWith #

This examples shows how to use ImageSprite and Ball colliding with each other and the edges of screen. See NOTE on args[0](0.md)


# Code Example #

Below is to shows how to use ImageSprite and Ball colliding using sdkBridger

```

package com.example;

import com.google.devtools.simple.runtime.components.Component;
import com.google.devtools.simple.runtime.components.HandlesEventDispatching;
import com.google.devtools.simple.runtime.components.android.*;
import com.google.devtools.simple.runtime.events.EventDispatcher;

public class BallAndImageSpriteActivity extends Form implements HandlesEventDispatching {

Canvas canvas;
Ball ball;
ImageSprite imageSprite;

void $define() {
canvas = new Canvas(this);
imageSprite = new ImageSprite(canvas);
ball = new Ball(canvas);

EventDispatcher.registerEventForDelegation(this, "test", "Initialize");
EventDispatcher.registerEventForDelegation(this, "test", "EdgeReached");
EventDispatcher.registerEventForDelegation(this, "test", "CollidedWith");
}


@Override
public boolean dispatchEvent(Component component, String id, String eventName, Object[] args) {
if (component.equals(this) && eventName.equals("Initialize")) {
initData();
return true;
} else if (eventName.equals("EdgeReached")) {
//Hits edges of screen
if (component.equals(ball)) {
ball.Bounce((Integer) args[0]);
ball.Heading(ball.Heading() - 22);
return true;
} else if (component.equals(imageSprite)) {
imageSprite.Bounce((Integer) args[0]);
imageSprite.Heading(imageSprite.Heading() - 22);
return true;
}
} else if (eventName.equals("CollidedWith")) {
//Ball and ImageSprite are colliding with each other
if (component.equals(ball)) {
// NOTE: args[0] will be of type Sprite

//Change its direction -- use static or random
ball.Heading(ball.Heading() - 22);
return true;
} else if (component.equals(imageSprite)) {
// NOTE: args[0] will be of type Sprite

//Change its direction -- use static or random

//Change its direction -- use static or random
imageSprite.Heading(imageSprite.Heading() - 55);
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

imageSprite.Picture("sp.jpg");
imageSprite.X(this.Width() / 2);
imageSprite.Y((this.Height() / 2) - (imageSprite.Height() / 2));
imageSprite.Speed(12);
imageSprite.Initialize();
imageSprite.Interval(32);
imageSprite.Enabled(true);

ball.Radius(22);
ball.PaintColor(COLOR_BLUE);
ball.Speed(12);
ball.Initialize();
ball.Interval(32);
ball.Enabled(true);


}

}

```