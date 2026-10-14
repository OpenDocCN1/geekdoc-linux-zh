
| ButtonMotionMask | KeyReleaseMask | SubstructureNotifyMask |
|---|---|---|
| ButtonPressMask | LeaveWindowMask | SubstructureRedirectMask |
| ButtonReleaseMask | OwnerGrabButtonMask | VisibilityChangeMask |
| ColormapChangeMask |  |  |

The names of the event-mask bits in Table 26.1 are generally, but not always, the same as the names of the event messages minus the suffix “Mask.” The KeyPress event, for example, is associated with the KeyPressMask bit mask. However, the Expose event is associated with ExposureMask. You just have to memorize these discrepant relationships. Table 26.2 shows all Xlib event types.

**TABLE 26.2  XLIB EVENT TYPES**

|  |  |  |
|---|---|---|
| ButtonPress | Expose | MapRequest |
| ButtonRelease | FocusIn | MotionNotify |
| CirculateNotify | FocusOut | NoExpose |
| CirculateRequest | GraphicsExpose | PropertyNotify |
| ClientMessage | GravityNotify | ReparentNotify |
| ColormapNotify | KeymapNotify | ResizeRequest |
| ConfigureNotify | KeyPress | SelectionClear |
| ConfigureRequest | KeyRelease | SelectionNotify |
| CreateNotify | LeaveNotify | SelectionRequest |
| DestroyNotify | MapNotify | UnmapNotify |
| EnterNotify | MappingNotify | VisibilityNotify |

Each event message is transmitted as a structure that contains information specific to that event. For instance, a mouse movement event carries with it the relative coordinate values of the mouse cursor’s “hot spot.” Other events carry different types of information such as a window’s position, or a keypress code. All event messages are declared in Xlib using C++ unions so that an event’s associated information is readily available. But this also implies that it is your responsibility to refer to the correct information for a specific event type. More on this subject in the next sections.

## Writing the Event Loop

Finally, the client application is ready to enter the section of code where it spends the rest of its runtime life—the event loop. Before explaining this important programming, it’s useful to review the steps that led to this critical juncture. So far, the xwelcome.cpp program has

- Connected to the X server by calling `XOpenDisplay()`
- Initialized window variables using macros such as `XDisplayWidth()`
- Obtained at least two contrasting color values through the BlackPixel() and WhitePixel() macros
- Created a window structure by calling XCreateSimpleWindow() and saving the function result in a Window ID variable
- Optionally specified a possible window title by calling XStoreName()
- Mapped the window by calling XMapWindow(), making the window potentially visible
- Specified the types of events the client wants to receive for this window by calling XSelectInput() with an appropriate event mask expression.

Every X client application performs most of the preceding steps in one fashion or another. After these steps, the program is ready to enter the infamous event loop, shown in Listing 26.2.

### LISTING 26.2 XWELCOME.CPP (EVENT LOOP)

```cpp
bool done = false;
XEvent event;
while (!done) {
    XNextEvent(display, &event);
    switch (event.type) {
    case Expose:
        cout << "Expose event received" << endl;
        break;
    case ConfigureNotify:
        cout << "ConfigureNotify event received" << endl;
        break;
    case KeyPress:
        cout << "Keypress detected" << endl;
        done = true;  // Exit on any keypress
        break;
    }
}
```

To provide a holding pen for each event as it arrives, the program declares a variable, here named event, of Xlib's XEvent structure data type. For a loop-control value, the program also declares a C++ bool variable, done, initialized to false. While this variable remains false, the event loop continues looping. There are other ways to write an event loop. Some programmers use a so-called "do-forever" for or while statement that repeats an indeterminate number of times. Regardless of how it's programmed, the event loop begins by obtaining the next event with the following statement:

```cpp
XNextEvent(display, &event);
```

Pass the global display pointer and a reference to the event structure as arguments. This deceptively simple statement performs three crucial activities:

- It retrieves the next event from the Xlib queue for the focused window of the indicated display.
