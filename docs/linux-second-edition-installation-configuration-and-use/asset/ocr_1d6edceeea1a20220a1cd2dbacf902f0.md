# fvwm (VIRTUAL WINDOW MANAGER) 277

Online information about the configuration of fvwm can be found in the very extensive man texts for fvwm, FwmIconBox, FwmPager, and FwmWinList.

If you want to try out a new configuration, the fastest and easiest way is to restart fvwm, which can usually be done by a menu command. At a restart, all X programs are preserved (including the editor to modify .fvwmrc).

The following paragraphs describe some particularly important keywords of the configuration file, without any completeness:

# ClickToFocus

A window only becomes active (gets the input focus) when it is clicked upon. If the keyword is prefixed with the comment character # a window gets the input focus as soon as the mouse is moved over it. At the beginning, this can be rather confusing, but it certainly saves a whole of mouse clicks. As already mentioned, ClickToFocus only works if NumLock is not active.

# AutoRaise n

Specifies the time in milliseconds after which a window is shifted to the top when the cursor is placed over it. This setting is useful when ClickToFocus is deactivated: in this case, after a short time, the active window also becomes the topmost window.

# IconBox x1 y1 x2 y2

Specifies the area where icons should be placed. Negative values refer to the right and/or bottom screen border.

# DesktopSize n, DesktopTopScale n, Pager x y

These three keywords control the size and position of the window for the virtual desktop. If this window irritates you and you only need one screen, you can comment out these three lines.

# OpaqueMove n

Specifies the percentage of screen size up to which windows are visibly moved together with them. With n=0, only the frames are moved, independently of the window size; this is the fastest way. If you have a fast computer (and above all a graphics card), you should try n=100 - it looks very impressive!

2.0 of fvwm is brimming with new functions, even more possibilities for configuration and visual layout and a slightly higher memory consumption. The popular GoodStuff module has been rewritten: it is now called FwmButtons. Windows can be “pinned” to the screen via the menu item STICK. The window is highlighted by horizontal lines in the title bar. When you work with a virtual desktop, the window is displayed on each desktop (whereas normal windows are only visible on the desktop where they were started).