# 6.4 Window managers

The appearance (the 'furniture') and the behaviour of the windows resembles the look and feel of a Window system. Under X, this part is implemented by means of the so-called window manager. The window manager under X is not part of the X Window system itself, but a client (application program), like any other.

This has the advantage that X itself does not (and cannot) make any prescriptions about look and handling, and even with 'busy' X client the system still reacts correctly.

Window managers determine the layout of the window's title bar, window frame, type of icons and, if needed, number of several virtual desktops. In addition, the window manager is responsible for the keyboard input. Depending on personal preferences, one can require a click in the window or to transfer the keyboard focus. Personally, I prefer the option in which the focus always belongs to the window where the mouse pointer is located.

There is a whole series of window managers with different properties, with the more recent ones following the 'Inter-client Communications Manual' (ICCM). The ICCCM is one of the official documents of the X Consortium which define the X Window system or the X environment. This documentation can be found on the Internet at ftp://ftp.x.org/xc/doc/specs/ICCCM. The ICCCM specifies the conventions with which applications have to operate with other clients (on the same server); the specifications laid down in the ICCCM can also be seen as a protocol. Critical points in this context are the interaction between window manager and applications, plus the selection mechanism (cut and paste).

Each of the available window managers has special functions and thus advantages and disadvantages. One useful feature is the representation of virtual screens or desktops which allows many windows to be neatly arranged on small monitors. Table 6.1 shows an overview of a series of widely used window managers. LINUX systems frequently use a program of the fwm family, which will be described in more detail in the next section.

| Program | Description |
| --- | --- |
| twm | 'Tab Window Manager': standard window manager in X11 |
| awm | 'Ardent Window Manager': preferred by hackers, has features (dynamic menus) that others do not offer |
| olwm | 'Open Look Window Manager': Sun’s window manager |