# # Real World Scenario

# ## Using Manufacturer-Provided Video Drivers

One of X's functions is to provide drivers that control the video card. XFree86, X.org-X11, and Accelerated-X all ship with a wide variety of drivers that support most video cards. Some cards, though (particularly very new ones), have weak support in the stock packages. XFree86 4.x and X.org-X11 both support a modular driver architecture, which means you can drop in a driver module for your card and, with minimal changes to your X configuration, use it without recompiling the main X package. Some video card manufacturers provide Linux video card drivers designed to work with XFree86 and X.org-X11. (Both X servers can use the same drivers.) Thus, if you have problems with the standard X video drivers, you may want to check with your video card manufacturer and the video card chipset manufacturers for Linux drivers.

Installing and using the manufacturer-provided video drivers is usually a matter of extracting files from a tarball and making a few configuration file changes. Sometimes manufacturers provide scripts that do this automatically. Consult the documentation that comes with these drivers for details. Many of these drivers are particularly helpful for enabling 3D acceleration features of modern cards. This support is most important for certain Linux games, but some non-game software can also benefit from 3D acceleration.

Note that some manufacturers have a habit of placing the standard Linux drivers (or, in this case, the standard XFree86 or X.org-X11 drivers) on their Web site. Thus, you should try to ascertain whether the drivers are genuinely different from what you already have before you bother installing them.

Users of video cards based on nVidia or ATI chipssets are most likely to benefit from using nVidia's or ATI's proprietary drivers, respectively. These drivers provide superior 3D and real-time video acceleration compared to the standard X drivers.

One problem with manufacturer-supplied drivers is that they're often proprietary. You might not have source code, which means the drivers might not work on more exotic CPUs, and the drivers could cease working with a future upgrade to your X server.

# ## Configuration Tools for XFree86 4.x and X.org-X11

Several configuration tools for XFree86 4.x and X.org-X11 are available:

The X server itself The X server itself includes the capacity to query the hardware and produce a configuration file. To do this, type **XFree86 -configure** (for XFree86) or **xorg -configure** (for X.org-X11) when no X server is running. The result should be a file called `/root/XF86Config.new` (for XFree86) or `/root/xorg.conf.new` (for X.org-X11). This file may not produce optimal results, but it's at least a starting point for manual modifications.