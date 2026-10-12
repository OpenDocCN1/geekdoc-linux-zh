# **386 Part III** CUSTOMIZING THE SYSTEM

+   	* The Language option allows international users to pick from one of several available languages. This is especially helpful to those users not intimately familiar with English but who still wish to use Linux.
+   	* The System option allows you either to reboot or halt the system. You don't need a password to execute these commands if physical access to the machine is allowed. Anyone sitting at the terminal login screen can thus either cause the machine to reboot or stop all processes, unmount the partitions, and power down the machine without corrupting files.

To read more about run levels and the default settings used by Red Hat, see Chapter 2.

If you wish to return to run level 3 or boot into a command-line interface, try running the Xconfigurator command again and not choosing the option of booting into X initially. If you do return to the GDM screen again and you wish access to the command line, you can always bring up another virtual terminal by pressing the Ctrl+Alt+F2 key combinations. For additional virtual desktops, try hitting any of the other F keys. To return to the GDM window from a command-line prompt, press Ctrl+Alt+F7, which is the default X virtual desktop.

# ## Running Xconfigurator

If you later decide to make changes to the manner in which you bring up the X server, several options are available. The easiest is a Red Hat utility, Xconfigurator. This program must run as root and you should run it at the console rather than in an X terminal session. Xconfigurator must test your video card's capability, and cannot do so effectively while in X. This program brings up a text-based session that walks you through the various settings for the video and monitor. First, the program determines the make of your video card, shows the results from the video test, and then offers you some possibilities to choose from as to the make and model of your monitor.

> **CAUTION**
> 
> Be sure to choose a monitor that best matches yours in terms of vertical and horizontal refresh rates. Setting your rates above that which your monitor can handle will overclock the display and might cause irreparable damage.