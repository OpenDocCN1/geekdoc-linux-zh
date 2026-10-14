# GETTING COLOR VALUES

Another important set of values concerns the background and foreground colors used for painting the window's display surface (sometimes called its canvas), and for displaying graphics and text. As mentioned, because X installations use a wide variety of output devices, a properly written X client can assume only that two contrasting colors are available. At a minimum, then, the following statements initialize two integer variables to the only two colors you can count on:

```
int intBlackColor, intWhiteColor;
intBlackColor = BlackPixel(display, intScreenNum);
intWhiteColor = WhitePixel(display, intScreenNum);
```

Despite the macro names BlackPixel() and WhitePixel(), the actual visible colors might not actually be black and white. In any case, however, they are guaranteed to be colors that the user can distinguish.

# CREATING AN X WINDOW

We now have enough information to create an X window. The simplest method for doing that is to call XCreateSimpleWindow() with the following arguments:

```
Window win =
XCreateSimpleWindow(
    display,
    DefaultRootWindow(display),    // Parent window
    intXPos, intYPos,              // Position
    intWidth, intHeight,           // Window width & height
    0,                             // Border width (default)
    intBlackColor, intWhiteColor); // Background, foreground
```

Assign the function result to a variable of type Window. This represents the window's ID number (probably as an unsigned long integer value) for future references to the window structure maintained by the X server. The first argument is the display pointer returned by XOpenDisplay(). Next comes the ancestor window, and because every window except the root must have a parent window, a valid parent-window ID is required by all new windows. In most cases, a client's main window lists the root window as its ancestor by calling the DefaultRootWindow() macro as shown, but this argument can be another Window ID value. After this information comes the position, width, and height of the window. As mentioned, these are merely hints to the window manager about where you want the window shown. Finally, specify the background and foreground colors obtained earlier. Optionally, reverse the two colors to produce a light-on-dark window interior.

> Tip
> Creating a window by calling XCreateSimpleWindow() or its more complex sister function XCreateWindow() does not display the window onscreen. This step merely prepares a Window structure in the X server. Several more statements, explained in the next sections, are required before the window becomes visible.