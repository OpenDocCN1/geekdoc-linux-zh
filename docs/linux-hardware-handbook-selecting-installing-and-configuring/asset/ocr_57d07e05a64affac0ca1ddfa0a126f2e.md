Some video cards support memory expansion, so you can buy a card with a small amount of RAM and expand that RAM at a later date. Unfortunately, RAM for such cards usually comes in proprietary formats, so it can be difficult to purchase RAM from anybody but the card's manufacturer. This results in grossly inflated prices for the RAM, even after the video card has become obsolete.

If you don't plan to make heavy use of OpenGL applications, there's little need to spend extra money on a video card that features huge amounts of RAM. 8MB will probably be plenty for any but the largest displays. If you want to use 3D graphics programs, though, you might want to get 32MB, 64MB, or even more on your video card.

# XFree86

Any decision you make concerning the purchase of a video card is inextricably linked to XFree86. Although there are other X servers for Linux, XFree86 is the one that ships with all Linux distributions, and the alternatives are commercial products. Therefore, relying upon an XFree86 alternative seldom makes economic sense, because it can substantially increase the cost of Linux video support. In most cases, XFree86 is adequate.

# Basic Design of XFree86

Linux's GUI environment is built up of several different layers. Many of the components that comprise each layer can be removed and replaced with equivalent components without disrupting the function of other layers of the system. Examples include

+   The X server
+   The X server contains what is, in most OSs, called the video driver. The X server can be written for one specific video chipset or family of chipsets (such as the XF86_S3V server for S3's VRGE series chipsets), or it can contain drivers for many unrelated chipsets (such as the XF86_SVGA server). The X server is the most important component of X when it comes to determining video hardware support.

+   X libraries
+   X programs usually rely upon program libraries, which are routines that are potentially useful to any program of a certain type. XFree86 includes a set of libraries that are required by X programs.

+   The window manager
+   A window manager controls the appearance of windows on the screen. Different window managers create different-looking drag bars, resizing controls, and so on. Window managers also handle the desktop—the background on which all windows reside. They usually include some means of launching programs from a pop-up menu. As a user, you can choose any of literally dozens of window managers for Linux. You can find out about many of the choices from http://www.p1iq.org/xwinman/.

+   X utilities
+   XFree86 comes with a large number of small programs that help make X a usable environment. For instance, the xterm program creates a window in which a text-based Linux shell runs, as shown in Figure 12.4.