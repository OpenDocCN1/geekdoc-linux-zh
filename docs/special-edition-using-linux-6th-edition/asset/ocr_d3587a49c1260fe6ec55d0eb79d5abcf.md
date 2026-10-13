GNOME used to ship with Enlightenment, but has recently switched to Sawfish, which is much lighter weight. It is also somewhat less configurable than Enlightenment, but then *everything* is less configurable than Enlightenment. In this section, we will discuss Sawfish. If you want more information on Enlightenment, see www.enlightenment.org.

Sawfish was developed in an effort to create an extremely configurable window manager (in the tradition of Enlightenment) with a small footprint. It has been fairly successful in this regard, though some Sawfish configuration still requires diving into its LISP-like configuration language. This section will focus on the majority of things that you can configure within the Control Center.

# SETTING FOCUS POLICY

*Focus policy* is how GNOME determines which window is currently active, and what to do when a window becomes active. The policies are as follows:

+   - **Click**—Windows only gain focus when you click them.
+   - **Enter-only**—Windows gain focus when you move into them (using the mouse pointer or using Alt+Tab or otherwise). Moving the mouse pointer onto the desktop does not cause the currently active window to lose focus. This is an incredibly useful focus policy because it allows you to type in one window while reading another window that might obscure it.
+   - **Enter-exit**—Windows gain focus only while the mouse pointer is within them. If the mouse points to the desktop, no window will have focus. This is generally not useful and is only provided for historical reasons.

The Focus Windows When They Are First Displayed setting determines whether new windows automatically get focus. Sometimes having new windows stealing focus can be very annoying, because you suddenly wind up typing in a different window. This is particularly frustrating when informational boxes steal focus. On the other hand, many people prefer not to have to explicitly give focus to every new window.

The Dialog Windows Inherit the Focus From Their Parent setting is very useful if you’ve turned off Focus Windows When They Are First Displayed. This means that if the window you are working in displays a dialog box, that dialog box automatically gains focus, even if new windows usually don’t. This is usually what you want.

Users accustomed to MacOS or Microsoft Windows sometimes have difficulty adjusting to the idea that window focus and window raising are separate. A window gains focus when keyboard input is directed to it. A window is raised when it appears on top of all other windows on the desktop. In the MacOS and Windows worlds, these two things are tied together, but not in GNOME (or UNIX in general). By turning off automatic raising, you can type in windows that are not on top. This is incredibly useful if you are reading in one small window and typing in a larger one.

Another problem with always raising the windows as they gain focus is that if you have Enter-Only or Enter-Exit focus policies and you move the mouse across the screen to select