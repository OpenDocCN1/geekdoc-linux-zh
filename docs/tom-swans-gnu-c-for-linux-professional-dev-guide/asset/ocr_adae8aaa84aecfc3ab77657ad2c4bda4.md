# LISTING 27.1 CONTINUED

```
while (!done) {
XNextEvent(display, &event);
switch (event.type) {
case ButtonPress:
cout << "ButtonPress event" << endl;
cout << "  button == " << event.xbutton.button << endl;
intMouseX = event.xbutton.x;
intMouseY = event.xbutton.y;
ShowMousePosition(gc, win, intMouseX, intMouseY);
break;
case ButtonRelease:
XBell(display, 50);  // i.e. 50% volume
break;
case MotionNotify:
intMouseX = event.xbutton.x;
intMouseY = event.xbutton.y;
ShowMousePosition(gc, win, intMouseX, intMouseY);
break;
case Expose:
ShowMousePosition(gc, win, intMouseX, intMouseY);
break;
case KeyPress:
cout << "Keypress detected" << endl;
done = true;  // Exit on any keypress
break;
}
}
```

Compile the xmouse.cpp program by changing to its directory and running make for the Makefile stored there. Enter these commands:

```
$ cd src/c27/xmouse
$ make
...
$ ./xmouse
```

# Note

Compile other programs in this chapter similarly. Also see the sidebar "Compiling X Clients" in Chapter 26, "Introducing X Programming."

Running the xmouse.cpp program displays a small window that shows the mouse pointer's location relative to the window (see Figure 27.1). Click and drag the mouse cursor inside the window to see other locations. Clicking and dragging is enabled only for Button1, but you can also click Button3. Releasing either button sounds a bell (which sounds more like a buzzer on my system). Press any key to end the program, or click the window's close button. The program reports events in the terminal window, showing button clicks and keypresses:

```
ButtonPress event
button == 1
ButtonPress event
button == 3
Keypress detected
```