# EXERCISE 6.1 (continued)

+   11.  Save the changes to the file, and exit from your editor.
+   12.  If X isn’t started, try starting it by typing **startx** at a text-mode command prompt.
+   13.  If X is already running, log out of your session and, if necessary, select an option to restart X or press Ctrl+Alt+Backspace to force X to quit and restart.

# Putting It All Together

XFree86 4.x and X.org-X11 require a section that’s not present in the XFree86 3.3.6 configuration file: `ServerLayout`. This section links together all the other components of the X configuration:

```
```
Section 'ServerLayout'
  Identifier    'single head configuration'
  Screen        "Screen0" 0 0
  InputDevice   "Mouse0" "CorePointer"
  InputDevice   "Keyboard0" "CoreKeyboard"
EndSection
```
```

Typically, this section identifies one **Screen** section and two **InputDevice** sections (for the keyboard and the mouse). Other configurations are possible, though. For instance, XFree86 4.x and X.org-X11 support *multi-head displays*, in which multiple monitors are combined to form a larger desktop than either one alone would support. In these configurations, the `ServerLayout` section includes multiple Screen sections.

# Obtaining X Display Information

Sometimes it’s helpful to know about the capabilities of your display, because it’s managed by X. The tool for this job is **xdpyinfo**. When you type **xdpyinfo**, the result is copious information about the current display, such as the X version number, the resolution and color depth of all the current displays, and so on. Much of this information is highly technical in nature, so you may not understand it all. That’s OK. I recommend you run this program and peruse the output to see what you can learn from it. If you should later want to obtain similar information on another computer’s display, you’ll know how to obtain it.

For still more technical information, you can use the `--ext extension` option to **xdpyinfo**. The *extension* is the name of an X extension, which is a software module that provides extended capabilities to X. (The basic **xdpyinfo** command, without any options, lists all the available extensions.)

You can obtain detailed technical information about a specific window with the **xwininfo** command. In basic use, you type **xwininfo**, move the mouse cursor over a window, and click. The result is a list of assorted data about the window you clicked, such as its size, location,