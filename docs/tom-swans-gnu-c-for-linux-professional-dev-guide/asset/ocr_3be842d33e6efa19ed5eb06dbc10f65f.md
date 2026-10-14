Keep in mind that a “display” comprises at least one or more screens, a keyboard, and a mouse. On Linux XF86 installations, the window manager may provide multiple screens selectable using the mouse or by pressing keys such as M-Tab (Alt-Tab). In the client program, however, only one Display-structure pointer is needed to access all the user’s input and output devices.

# PREPARING WINDOW ATTRIBUTES

Before creating and displaying a window, most X clients need some information about the state of the display such as its dimensions and color values. Most such values are easily obtained by using Xlib macros to extract members of the Display data structure. For example, xwelcome.cpp uses the following three macros to find out some information about the display maintained by the X server:

```
int intScreenNum = DefaultScreen(display);
int intDisplayWidth = DisplayWidth(display, intScreenNum);
int intDisplayHeight = DisplayHeight(display, intScreenNum);
```

The first statement assigns to integer intScreenNum the number of the display’s default screen. This screen number is then used in two more macro calls to find the width and height of the screen in pixels. The reason for using macros such as DefaultScreen() and DisplayWidth() is because the contents of the Display data structure are intended to remain “opaque.” Not referencing these members directly allows Xlib’s programmers to change the members’ names without affecting X client programs. Always use macros as shown here to access Display-structure members. This helps protect your code from future changes to Xlib.

> Tip
> It’s a good idea to adopt useful naming conventions for your program’s variables. For example, xwelcome.cpp prefixes its integer variables with int. Xlib contains an overwhelming number of declarations, function names, structures, and other elements, and it’s a good idea to choose program identifiers that describe both their type and purpose. All Xlib functions, by the way, begin with a capital X, so you probably should not do the same with your program’s functions.

Using the display parameters determined so far, the xwelcome program calculates the approximate width, height, and position of its window with these statements:

```
int intWidth = intDisplayWidth / 3;
int intHeight = intDisplayHeight / 8;
int intXPos = 0;
int intYPos = 0;
```

These steps prepare for creating a window one-third the width of the screen, and one-eighth its height. The window’s initial position is determined by the window manager, so the two position variables are simply zeroed. Always keep in mind that, due to differences among X installations, all specifications such as window sizes and positions are mere hints to the window manager, which is free to arrange windows in any way it sees fit.