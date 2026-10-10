# 5.3 X Window Configuration with Metro-X

By special arrangement, a license to install a single copy of the Metro-X enhanced X server is included with the Official Red Hat Linux/Intel CD. Please note that, unlike the XFree86 server (also included), Metro-X is commercially licensed software. You should review and accept its license terms before installing it. Metro-X supports many video cards that are not supported by XFree86. The configuration utility can be run in graphical mode (configX) or text mode (configX.curses).

# 5.3.1 System Requirements

8 megabytes of RAM minimum; 16 megabytes are recommended. The base server package requires 12 megabytes of disk space.

# 5.3.2 configX.curses

**configX.curses** is a simple graphical configuration tool for configuring Metro-X. The **configX.curses** utility does not provide support for configuring multiple screens or choosing the number of buttons on your mouse. If you need these facilities you must use **configX**. To run **configX.curses** type the command:

```
configX.curses
```

The opening screen has information on Metro Link, Inc. and brief instructions on what you will need to configure Metro-X. Press the **Enter** key to begin the configuration. The screen will display the current configuration information at the top and the configuration menu at the bottom. Use the arrow keys to move the highlight up and down the menu and the **Enter** key to select the highlighted item.

# Graphics Card

When you select **Graphics Card** from the configuration menu, a list of supported cards will be displayed. Select your video card as above. After