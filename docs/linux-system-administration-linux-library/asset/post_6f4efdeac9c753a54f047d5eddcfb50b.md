
# Configuring an X Server

- You can start multiple X sessions as different users, complete with a different desktop-environment and assorted X customizations. This can be useful when testing different environments or when debugging a particular user's configuration.

# Configuring an X Server

Configuring X entails making adjustments to one primary file: XF86Config. This file resides in the /etc/X11 directory on Red Hat systems, but some distributions place the file in /etc. You can configure X by directly editing this XF86Config file or using an X configuration tool. In most cases, X is configured reasonably during system installation, but sometimes the installation routines bundle it. You might also need to adjust the configuration to change configuration details or if you change your video hardware.

Most Linux distributions released in the latter half of 2000, including Red Hat 7.0, ship with two versions of XFree86: 3.3.6 and 4.0 or 4.0.1. XFree86 3.3 is stable and supports a large number of video cards. XFree86 4.0 is less tested and supports fewer video cards, but it includes additional features, such as the ability to bind two video cards' displays into a single desktop. For the average user, it's best to leave the X configuration as whatever your distribution selected. In some cases, though, you might want to upgrade to XFree86 4.0 (or downgrade to 3.3.6). Consult the main XFree86 Web site (http://www.xfree86.org) to learn more about the differences between these two versions of XFree86.

> NOTE Some distributions, such as Red Hat 7.0, install components of both versions of XFree86. Typically, the font and support files from version 4.0 are installed, with a server file for version 3.3.6. This setup may seem strange, but it works. The 3.x configuration instructions when adjusting a system are:

## XFree86 3.x

XFree86 3.x (including the latest, and perhaps last, in that line, 3.3.6) has long been the standard X server in Linux. You can configure XFree86 3.x through its XF86Config file or by using any of several configuration tools. This section describes this configuration, so that you can adjust your system's settings when need arise.

To determine whether your system is running XFree86 3.x, check for a link to an X server in /etc or /etc/X11 directory. In Red Hat 7.0, this link is called /etc/X11/X. If this link points to a file named XFree86, the system is configured to use XFree86 4.0. If the link points to a file named XF86_Server, Server is a server name such as SVGA or Mach64, the system is configured to use XFree86 3.x.

![](img/4fb617eb648f87def380ef5d92052d01_572_0.png)

## The XF86Config File

The XF86Config file contains settings that are grouped into several different sections (you may want to load this file into a text editor to review your settings while reading the following):

- Files: The Files section includes paths to directories that contain important files. Most important of these are the FontPath mice, which point X to its font files and servers, as described shortly.

- ServerFlags: You can set a few miscellaneous controls in this section. Chances you won't need to make any adjustments here.

- Keyboard: This section defines the keyboard. Aside from the keyboard repeat rate, which you may want to adjust via the AutoRepeat line, these are mostly things you don't need to adjust.

- Pointer: Your mouse's settings are set in this section. The Protocol specifies the type of mouse you're using—PS/2 for most modern PS/2-interface mice, Microsoft for Microsoft serial mice, and so on. (The XF86Config man page includes information on the allowable values for this option.) You specify the device file to which the mouse is attached using the Device line. Mistakes on these two lines are common sources of X difficulties. If incorrectly, X won't start, will start without any pointer, or will start, but you won't be able to move the mouse pointer.

- Monitor: This section defines the characteristics of your monitor. Most important of these are the HorizSync and Refresh lines, which define horizontal and vertical rates. (Note: OCR text was fragmented here, reconstructed based on context).

- Device: The XF86Config file contains one or more Device sections. You may need to do the same, or specify the mouse device directly.

- Screen: There are usually Screen sections, which define the monitor. (Note: OCR text reconstructed).

- DefaultDepth: This option sets the color depth. (Note: OCR text reconstructed).

## Configuring an X Server

- You can start multiple X sessions as different users, complete with a different desktop-environment and assorted X customizations. This can be useful when testing different environments or when debugging a particular user's configuration.

Most Linux distributions released in the latter half of 2000, including Red Hat 7.0, ship with two versions of XFree86: 3.3.6 and 4.0 or 4.0.1. XFree86 3.3 is stable and supports a large number of video cards. XFree86 4.0 is less tested and supports fewer video cards, but it includes additional features, such as the ability to bind two video cards' displays into a single desktop. For the average user, it's best to leave the X configuration as whatever your distribution selected. In some cases, though, you might want to upgrade to XFree86 4.0 (or downgrade to 3.3.6). Consult the main XFree86 Web site (http://www.xfree86.org) to learn more about the differences between these two versions of XFree86.

## Using an X Configuration Tool

All major Linux distributions include tools that run during system installation. These tools are usually available after installation. Examples include:

- f86config: The crudest of the common configuration tools. It runs entirely in text mode and asks you a series of questions about hardware and desired configuration.

- Xconfig: Another text-mode tool. Unlike f86config, though, Xconfig uses text dialogs rather than simple streams.

- F86Setup: This utility works only when X is running. Most distributions, including Red Hat, use GUI configuration tools similar to XF86Setup to configure the system initially. These work because the setup routines the lowest-common-denominator VGA server, which works on all but the most ancient displays.

## Figure 16.2 GUI configuration tools let you select options using list boxes, buttons, and so on.

![](img/4fb617eb648f87def380ef5d92052d01_575_0.png)

You should have several pieces of information handy before you begin configuring your X server. Although some configuration utilities can probe for some of this information, you'll need to know some of it yourself. These critical features are as follows:

- Mouse type: Most modern computers use a PS/2 mouse, but there are several other options (displayed near the top of the window in Figure 16.2).

- Mouse device: Most distributions create a link so that you can access a mouse as /dev/mouse. You may need to do the same, or specify the mouse device directly. /dev/psaux is the usual device file for PS/2 mice. Serial mice can usually be addressed as /dev/ttyS0 or /dev/ttyS1.

- Video card information: Some configuration utilities let you select a card from a long list of model names. Others require you to know the chipset used on the card.
