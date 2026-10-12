The X Window System for Red Hat Linux comes from the XFree86 Project; see the XFree86 home page at `http://www.xfree86.org/~`. The XFree86 Project consists of a group of programmers who maintain the free version of the X Window System for Intel-based PCs. As a result, the Linux version of X is called XFree86.

# ### Understanding the X server

At the heart of X is the X server, which is a process or program just like any other, such as the vi editor or a calendar program. Rather than editing text or telling you the date, though, the X server application provides the fundamental services necessary to create and manage a graphical interface. These services include controlling the video adapter; interpreting input from keyboards, mice, and other input devices; drawing windows; moving them around, scribbling in them; and responding to requests from X clients.

X clients are the typical sort of applications, such as word processors, Web browsers, or e-mail programs that run in the graphical environment the X server maintains. When X clients need to display output or show a dialog box, they do so by communicating with the X server, which is solely responsible for drawing on the screen. X clients rely on the X server for screen output because they have no independent capability to do so.

Finally, the X server runs on your computer and controls the monitor, keyboard, and mouse. X clients, on the other hand, may run locally or on remote systems.

Configuring X requires you to create the server's configuration file, `/etc/X11/XF86Config` or similar. This file contains information about your video card, monitor, keyboard, mouse, and other input devices. Red Hat Linux comes with XFree86 version 4.0.3, which itself includes a configuration utility named `xf86cfg`, which simplifies creating a working configuration file.

In Session 2, you learned how to use the Xconfigurator utility to create the X configuration file.

The next part of this session walks you through the X configuration process using the xf86cfg program so that you can see the configuration options in detail, and understand the format and purpose of the configuration file. If the X server installs incorrectly configured X or if you would like to experiment with your X configuration, you can use `xf86cfg` and the information in the next part of this session to reconfigure X using the new XFree86 configuration tool, `xf86cfg`.

# **Using xf86cfg**

To run `xf86cfg`, log in as `root` and type `xf86cfg` at the shell command prompt or in a terminal window, if X is already running. (The rest of this session assumes that you are using `xf86cfg` while running X.) The initial screen should resemble Figure 21-1.