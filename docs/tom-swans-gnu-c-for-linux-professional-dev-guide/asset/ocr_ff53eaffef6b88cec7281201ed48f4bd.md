```
case ConfigureNotify:
    intWidth = event.xconfigure.width;
    intHeight = event.xconfigure.height;
    break;
```

That's usually all you need to do to scale graphics—provided, that is, your graphics are drawn relative to window's size. You don't have to redraw graphics in response to this event. Just draw them as usual in response to an Expose event.

> Note
> Attempts to prevent users from resizing a window are strongly discouraged. It takes a little more work to scale graphics as described here, but users will appreciate your efforts in keeping your X applications as unrestrictive as possible.

# ATOMIC ENERGY

Chapter 26, “Introducing X Programming,” mentioned the topic of atoms. You may not need to use atoms in every application, but they are highly useful for specifying certain types of information and also for communicating between clients. The following sections explain how to create and use atoms.

# SETTING AND GETTING ATOMS

In X programming, a property is a synonym for an atom. You have already seen one such atom, used to suggest a window title to the window manager. To assign a string for this purpose, programs such as xrainbow.cpp (refer to Listing 28.2) execute the following statement:

```
XStoreName(display, win, "X Rainbow");
```

That stores a copy of the specified string in the X server for this window and display. The string is in this case identified by the atomic symbol XA_WM_NAME. Other atomic symbols, all of which are capitalized beginning with XA, are found in the file Xatom.h in standard X11 include path. A specific string such as the suggested window title here is associated with its atomic symbol and a window ID; therefore, each window can have its own identically named atoms.

> Note
> As mentioned in the preceding chapters, a window title identified by the XA_WM_NAME atom is merely a suggestion or “hint” to the window manager. There is no guarantee that the window manager will actually display the title at any specific location, or at all. (Any window manager worth using, however, ought to at least make an attempt to display the window's title.)

Given any Window ID, you can obtain the name assigned to that window by calling XFetchName(). Use programming such as this (assume win is the Window ID):

```
char *wname = NULL;
if (XFetchName(display, win, &wname))
    cout << 'Name is ' << wname << endl;
```