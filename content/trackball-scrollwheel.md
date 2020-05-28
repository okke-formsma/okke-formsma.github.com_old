Title: Using a trackball as scrollwheel
Date: 2020-05-27 19:35
Categories: 


Tiny scrollwheel on mice have a few problems. They are small and the movement to scroll is prone to RSI. I've been using an Elecom HUGE trackball, and I love it. Except it doesn't have a nice scroll ring as the Kensingtons have. Today I figured out how to turn the entire trackball into a huge scrollwheel by configuring libinput.

To try it out, run a few xinput commands. 

1. `xinput list` and find the device id of your mouse. In my case it's 14.
2. `xinput set-prop 14 "libinput Scroll Method Enabled" 0, 0, 1` to enable 'button scrolling'
3. `xinput set-prop 14 "libinput Button Scrolling Button" 12` to use 'Fn3' on the Huge as the scroll trigger. If you want to use the 'middle mouse button', use 2 here.

If you like it, create the file /usr/share/X11/xorg.conf.d/60-huge.conf to make these settings persist between reboots.

```text
Section "InputClass"
    Identifier  "ELECOM TrackBall Mouse HUGE TrackBall"
    Option  "ScrollMethod" "button"
    Option  "ScrollButton" "12"
EndSection
```

