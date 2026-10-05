Applications, such as Web browsers, text editors, and so forth, request that the window manager provide windows with specific user controls (check boxes, buttons, scroll bars, and so forth) in specific positions. The window manager, in conjunction with any GUI widget toolkits in use, then composes the requested window for the user.

The X server is capable of keeping track of multiple video cards, monitors, and input devices. Therefore, an X server is capable of logically interfacing with a large array of displays. In a multi-display configuration, X can be configured to present the displays as individual displays or as one large display, or as multiple logical groupings of one or more displays. See Figure D-3.

![](bbox=[0.268, 0.303, 0.841, 0.715])

Figure D-3 Standard single-user X server

Figure D-3 shows a typical single-station X implementation that uses a single server to handle a single keyboard/mouse input and outputs a single desktop to one or more monitors.

See Figure D-4 on page 311.