The *x* and *y* offsets specify where to place the window. If *x* is a number preceded by **+**, the left edge of the window is placed *x* pixels from the left edge of the screen. If it is a number preceded by **-**, the right edge of the window is placed *x* pixels from the right edge of the screen.

If *y* is a number preceded by **+**, the top edge of the window is placed *y* pixels from the top edge of the screen. If it is a number preceded by **-**, the bottom edge of the window is placed *y* pixels from the bottom edge of the screen.

+   * -iconic Indicates that the window should start up ''iconified"" rather than open.

# xterm

*xterm* is a terminal emulator for the X Window system. It is testament to (some would say indictment of) UNIX's command-line heritage that one of the most popular graphical applications is a terminal emulator. To start an *xterm* session, simply type:

```
$ xterm &
```

It's usually convenient to put the command in the background so you get your original shell prompt back.

An *xterm* emulates a VT-102 terminal, which was a popular serial terminal used on multiuser systems in times gone by.

*xterm* is pretty simple without too many flashy features. However, it does offer some features above what the original VT-102 offered.

# Font Selection

To change the *xterm* font, press Ctrl and click mouse button 3. You are given a choice of several font sizes, ranging from unreadable to huge. Pick the one you want.

# VT Options

VT options are options that control various aspects of the terminal's behavior. For example, you can enable a scrollbar on the left-hand side of the terminal, turn on reverse video, or switch between abrupt and smooth scrolling.

To change the VT options, press Ctrl and mouse button 2. A menu of various options appears, allowing you to change aspects of the terminal's behavior. Most times, you'll leave the settings alone.