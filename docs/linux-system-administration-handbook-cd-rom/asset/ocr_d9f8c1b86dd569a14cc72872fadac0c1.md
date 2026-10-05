# 16.4 Using the X Window Managers

+   + "Start twm" Restart /usr/X1R6/bin/twm
+ "Start MWM" Restart /usr/X1R6/bin/mwm
+ "Start olwm&mini-olwm.xpm*" Restart /usr/openwin/bin/olwm
+ "Start olwm&mini-olwm.xpm*" Restart /usr/openwin/bin/olwm
**
+ "Yes, Really Quit&mini-excl.xpm*" Quit
+ "No, Don't Quit&mini-cross.xpm*" Nop

# Modules

One of the reasons that everyone likes fwm2 so much (besides the config- urability, cheap price, number of people who have configuration files, look and feel of Windows 95, etc.) is the fact that many functions of fwm are in modules that don't always have to be loaded in memory. This allows one con- figuration to have a very bare-bones setup, while another setup may have all the bells and whistles (literally).

Modules get started either in the .fwmrc file or can be started from the menu. Here's some of the major modules you'll see in fwm2:

pager—Sets a virtual desktop, allowing you to have multiple desktops to work in. fwm can also be configured to start specific programs in specific virtual desktops for easier use.

task bar—This is one of the critical parts of fwm2-95. The task bar acts very much like the task bar of Windows 95, giving a list of running pro- grams, the current time, status of any incoming E-mail, and the ever- popular star menu.

buttons—If you look above the task bar in fwm2-95, you'll see a series of buttons, a clock, and the desktop (the pager module). This is the button module, and it cannot only create buttons to start pro- grams (Netscape, xterm, etc.) but it can also have the output of some programs running inside it. The clock and the FVWM pager are two examples of this. Some users have CD players, system load programs, and other programs running within the buttons. As with most FVWM functions, the size, style, contents, and location of the buttons can be set from within the fwmrc file.

audio—Yes, if you choose, you can have FVWM make noises when you do things within FVWM (opening windows, starting FVWM, stopping FVWM, etc.).

auto—This module allows you to automatically “raise” (bring to the front) a window after a certain amount of time. The window must have the focus for the allotted time before the window gets raised.