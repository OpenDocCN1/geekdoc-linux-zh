**NOTE:** If you aren't familiar with pico, don't worry. All of the available commands are always shown at the bottom of the screen. Any command that **starts** with the carot symbol (`^`) means you use the CTRL key along with other keys specified. For example, `^X` means CTRL-X.

Most likely, the file will be empty. If that is the case, simple add the following content:

```
#!/bin/sh
startkde
```

If the file is not empty, go to the very last line. It will probably begin with the string "exec," which tells the system to execute a program. Change that line so that it reads "startkde" instead.

# KDE Basics

KDE shares many qualities with other graphical desktops, such as Windows or MacOS. It has a desktop on which files and folders can exist. One key point to note is that because Linux places all the hard disks on the system into a unified directory tree, you won't find a special icon allowing you to browse a particular disk like you can under "My Computer." 
At the bottom of the screen, you will find KDE's panel. The left-most K button is the equivalent of the Windows Start Button. By clicking on it, you will be presented with a menu showing you a number of applications that are startable by simply clicking on the appropriate menu entry.

What makes the panel different from the Windows Start menu is that it is also a shortcut bar to commonly used applications. You can configure the bar to have any shortcuts you like by clicking on the K button and selecting Panel. Under this menu is a number of configuration options.

If you want to hide the panel altogether, you can do so by clicking on the arrows on the far-right or the left side of the panel. This will make the panel hide in that direction. Click on the arrow again to bring the panel back.

# The KDE Control Center

The KDE Control Center is a lot like the Control Panel for Windows, except it is specifically geared toward desktop configuration items (see Figure 3-3).
The Control Center offers an impressive array of tools for configuring KDE to heart's delight. This includes support for a variety of themes, colors, background, screen savers, certain applications, and certain types of hardware. The best way to see all that has to offer is to go through it and play—this is one of the rare opportunities you have as a system administrator to play with the interface without breaking your system.
In this section, we will step through several common tasks. They should give you an idea of what can be done and the typical method for figuring out how to do it. As mentioned earlier, the interface is very Windows-like, so getting around in it should be relatively easy.