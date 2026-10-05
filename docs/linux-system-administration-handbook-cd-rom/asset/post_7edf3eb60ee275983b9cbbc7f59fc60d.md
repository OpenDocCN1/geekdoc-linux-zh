
# Focus

There are three ways to determine which window has the “focus,” that is, what window will be controlled by the keyboard. The first method is the one you're most familiar with—click in the window to make it the active window. This is called “Click to Focus” and it is turned on by the .fwwm file with the following:

*** ClickToFocus

The other two methods, Mouse Focus and Sloppy Focus, are very similar. Mouse Focus means wherever the mouse pointer is the control. Sloppy Focus is the same as Mouse Focus, with the exception that if the mouse pointer leaves the window but does not enter another window (for example, goes to the root window), the window you were just in remains focused. You can run on this focus method with either of these options:

*** MouseFocus

*** SloppyFocus

# Menus

Besides the regular start menu that has the same configurability as the Windows 95 start menu, there are also menus available if you left-click on the root window. These menus are also defined in the .fwwm file. The menus are pretty much self-documenting. The “AddToMenu” line adds a menu definition called “Quit-Verify” that has a title of “Really Quit Fvwm”

The next lines define the items in that menu. The + at the beginning of the line means it’s part of the menu, followed by the text in the menu. You can include an icon in this if you enclose the name in %. The last part of the menu line is the actual command. The “Restart” in this menu means to quit fwm and start the named program. This allows you to quit fwm and start another manager. If a menu option has no text and has an action of “Nop”, then it will create a separator in the menu. Replacing the “Restart” with “Exec” will start the new program without quitting fwm—but it’s not a good idea to start multiple window managers.

```
#n# This menu is invoked as a sub-menu—it allows you to quit,
# restart, or switch to another WM.
#
AddToMenu "Quit-Verify" "Really Quit Fvwm" Title
+ "Restart@mini-turn.xpm*" Restart fwwm95-2
+ "Nop* Thiel
```

# 16.4 Using the X Window Managers

+ "Start twm" Restart /usr/X1R6/bin/twm
+ "Start MWM" Restart /usr/X1R6/bin/mwm
+ "Start olwm&mini-olwm.xpm*" Restart /usr/openwin/bin/olwm
+ "Start olwm&mini-olwm.xpm*" Restart /usr/openwin/bin/olwm
**
+ "Yes, Really Quit&mini-excl.xpm*" Quit
+ "No, Don't Quit&mini-cross.xpm*" Nop

# Modules

One of the reasons that everyone likes fwm2 so much (besides the config- urability, cheap price, number of people who have configuration files, look and feel of Windows 95, etc.) is the fact that many functions of fwm are in modules that don't always have to be loaded in memory. This allows one configuration to have a very bare-bones setup, while another setup may have all the bells and whistles (literally).

Modules get started either in the .fwmrc file or can be started from the menu. Here's some of the major modules you'll see in fwm2:

pager—Sets a virtual desktop, allowing you to have multiple desktops to work in. fwm can also be configured to start specific programs in specific virtual desktops for easier use.

task bar—This is one of the critical parts of fwm2-95. The task bar acts very much like the task bar of Windows 95, giving a list of running programs, the current time, status of any incoming E-mail, and the ever popular star menu.

buttons—If you look above the task bar in fwm2-95, you'll see a series of buttons, a clock, and the desktop (the pager module). This is the button module, and it cannot only create buttons to start programs (Netscape, xterm, etc.) but it can also have the output of some programs running inside it. The clock and the FVWM pager are two examples of this. Some users have CD players, system load programs, and other programs running within the buttons. As with most FVWM functions, the size, style, contents, and location of the buttons can be set from within the fwmrc file.

audio—Yes, if you choose, you can have FVWM make noises when you do things within FVWM (opening windows, starting FVWM, stopping FVWM, etc.).

auto—This module allows you to automatically “raise” (bring to the front) a window after a certain amount of time. The window must have the focus for the allotted time before the window gets raised.

# KDE

In case you ever wanted the functionality that Windows 98 is supposed to have without all the excess Microsoft baggage, there's KDE. The beta we're using to write this section (Beta3) seems to be more stable and a magnificent for first-time users. Like Windows 98, many of the functions of the desktop are integrated, with drag and drop capabilities, and there a a heavy dependence on browsers. KDE comes with its own HTML browser that, while not as full featured as something like Netscape, does the quit quite well. The only drawback is that for applications to take full advantage of KDE, they must be integrated.
