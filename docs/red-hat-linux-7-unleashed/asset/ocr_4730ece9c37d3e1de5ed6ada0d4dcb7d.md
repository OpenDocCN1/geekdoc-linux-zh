Scroll through your .fvwm2rc file until you find the default Key definitions:

```
# some simple default key bindings:
Key Next A SCM Next [ ] Focus
Key Prior A SCM Prev [ ] Focus
```

Add the following cursor key definitions:

```
# Shift + Ctrl moves 1 page in direction
Key Left A CS Scroll -100 +0
Key Right A CS Scroll +100 +0
Key Up A CS Scroll +0 -100
Key Down A CS Scroll +0 +100
```

These definitions define Shift+Ctrl+CursorX, which will shift your desktop to the next available desktop in X direction. This means that you can move between desktops without using a mouse! Next, insert the following definitions:

```
# Alt + Shift move 1/10 page in direction
Key Left A MS Scroll -10 +0
Key Right A MS Scroll +10 +0
Key Up A MS Scroll +0 -10
Key Down A MS Scroll +0 +10
```

These definitions define Alt+Shift+CursorX, which will shift the current desktop in the designated X direction. This means that you can work using clients whose windows exceed the current desktop borders by shifting the screen! Finally, add what is perhaps the most useful definition:

```
# Alt + Ctrl move cursor 1/100 page in direction
Key Left A CM CursorMove -1 +0
Key Right A CM CursorMove +1 +0
Key Up A CM CursorMove +0 -1
Key Down A CM CursorMove +0 +1
```

These definitions define Alt+Ctrl+CursorX, which will move your mouse pointer 1/100 the width of the current page in the designated direction. This is fine enough resolution to handle nearly every desktop. After making the changes, use fvwm2's root menu (by clicking the left mouse button in a blank area of the desktop) to restart the window manager. This will put your changes into effect right away.

You'll probably also want to define additional keys (such as FKeys) in conjunction with Alt or Ctrl, to mimic mouse button presses or root menu operations. This is a handy way to create a pointercless X11 environment! Pointers on creating your own definitions can be found in the fvwm2 man page.

![](bbox=[0.9, 0.75, 0.99, 0.95])