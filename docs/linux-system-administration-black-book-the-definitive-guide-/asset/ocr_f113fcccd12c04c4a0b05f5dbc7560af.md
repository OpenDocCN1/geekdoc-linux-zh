# ## Window Managers

One item installed on the client side is the *window manager*. This tool manages window movement, iconification, and resizing, but not the actual drawing and look of the windows. A window manager is not the actual X client, however. Instead, it is an intermediate program, taking window movement instructions from the server and translating them into actual motion.

As the system administrator, you are not saddled with the task of fully customizing every user's environment. However, because you know what your user base will be, you may want to set a default working environment that makes sense to the users. Choosing a window manager—whether you stick with the defaults or use something new—is part of this task. The default window manager provided with the GNU Network Object Model Environment (GNOME) in Red Hat is Enlightenment (\[www.enlightenment.org\]). The K Desktop Environment (KDE) uses its own window manager by default. Other popular choices are:

+   * AfterStep (**www.afterstep.org**)
+   * Blackbox (\[http://portal.alug.org/blackbox/\])
+   * IceWM (\[http://icewm.cjb.net\])
+   * Sawmill (\[www.dcs.warwick.ac.uk/~johnt/sw/sawmill/\])
+   * Window Maker (**www.windowmaker.org**)

Some of these items actually come on the Red Hat CD-ROM—AfterStep and Window Maker to be specific. Installing the included window managers requires the following RPMs, listed in the order you need to install them:

+   * AfterStep—AfterStep-1.8.0-1.i386.rpm
+   * Window Maker—libPropList-0.9.1-1.i386.rpm, WindowMaker-0.61.1-2.i386.rpm, and wmakerconf-2.1-1.i386.rpm
+   * Sawmill—(If you are running GNOME) Sawmill-gnome-0.24-3.i386.rpm, sawmill-0.24-3.i386.rpm

# ## Display Managers

The other side of the X client coin is the *display manager*. This tool manages the look and feel of your desktop. The feel includes such issues as user logins, because people can log in and out of their sessions without ever leaving the GUI. You generally do not run out and replace your display managers as often as you might your window managers. Three display managers are common, and they each come with Red Hat Linux:

+   * *gdm*—GNOME's display manager.
+   * *kdm*—KDE's display manager.
+   * *xdm*—The X display manager.