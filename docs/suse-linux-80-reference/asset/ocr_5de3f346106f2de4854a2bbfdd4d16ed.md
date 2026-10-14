# Changes

XFree86-4.0 is, of course, based on the version 3.3.x. Unfortunately, not all drivers are included, as some are very complex and could not be ported to the new XAA architecture. If these graphics cards were supported by SuSE Linux before, you can still use these with the XFree86 version-3.3.x. Use SaX to configure these cards.

The graphics cards concerned here are those previously used with the following X servers: XF86_S3, XF86_Mach8, XF86_Mach32, and XF86_8514.

In the case of S3 cards, those that previously required the S3 server are not supported by XFree86-4.0. Those that previously worked with the SVGA server will work correctly with XFree86-4.0. Basically these are the graphics cards S3 Trio3D, Savage4, Savage3D, and Savage2000 chips and almost all 3Dfx Voodoo cards. Graphics cards that needed the other X servers listed above (Mach8, Mach32, and 8514) are no longer very common. For these graphics cards—as for all the old S3 cards—the XFree86-3.3 version continues to be available.

# Configuration of the X Window System with SaX2

# Differences Between the X Server and the Window Manager

In Linux, a graphical interface is any component that ensures all necessary hardware components are supported. This service is referred to simply as the X server.

The graphical interface, the X server, allows your hardware to communicate with your software. This is how desktops like KDE and GNOME can display information on screen with which the user can interact. These desktops and similar applications are often called window managers. In Linux, there are several window managers, which can differ greatly in appearance and performance.

Without a functioning graphical interface—without an activated X server—there would be no graphical user environment. SuSE offers the application SaX2 to ease the configuration of your graphical interface as much as possible.

# About SaX2

The application SaX2 (SuSE Advanced X11 Configuration) is responsible for the setup of X Window System, the graphical user interface. SuSE Linux finds itself in one of these states following a standard installation: