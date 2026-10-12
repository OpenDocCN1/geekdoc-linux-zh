card) — either a plug-in card or some circuitry built into the system’s mother-board — that causes the output to appear on the monitor.

![](bbox=[0.17, 0.2, 0.28, 0.27])

The X Window System for Red Hat Linux comes from the XFree86 project — a cooperative project of programmers who bring X to the PC. (You can access the XFree86 home page at http://www.xfree86.org/.) As a result, the Linux version of X is called XFree86.

# Understanding the X server

At the heart of X is the X server — a process (computer program) running on a computer that has a bitmaped display, a keyboard, and a mouse. Applications (X clients) that need to display output do so by communicating with the X server via one of several possible interprocess communication mechanisms.

When you run X on your system, the X server runs on your computer and controls the monitor, keyboard, and mouse. The server responds to commands sent by X clients that open windows and draw in those windows. The X clients may run locally or on remote systems.

The X server configures the display (number of colors, resolution in terms of number of pixels horizontally and vertically), mouse, and keyboard based on information stored in a configuration file. Red Hat Linux comes with two versions of XFree86 — 3.3.6 and 4.0.1. Depending on your video card, the installation program selects an X server from one of these versions of XFree86. Each version has a different configuration file. For XFree86 3.3.6, the configuration file is `/etc/X11/XF86Config`. For XFree86 4.0.1, the configuration file is `/etc/XFree86Config-4`.

Configuring X requires you to prepare the configuration file. The configuration file contains information about your video card, monitor, keyboard, and mouse. Red Hat Linux comes with a utility program called `xf86config` (same name as the configuration file, but in lower case) that enables you to create the `XF86Config` working configuration file.

![](bbox=[0.17, 0.75, 0.28, 0.82])

You don’t need to create the X configuration file with the `xf86config` program if when you install Red Hat Linux (following the instructions outlined in Sessions 1 through 3), the installation program automatically detects your system’s video chipset and enables you to configure X through a number of dialog boxes. Additionally, Session 4 shows you how to run the `Xconfigurator` utility to create the X configuration file.