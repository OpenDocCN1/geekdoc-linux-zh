
## Part III

### TABLE 12.1 Continued

| Resolution | 8 bpp | 16 bpp | 24 bpp | 32 bpp |
| :--- | :--- | :--- | :--- | :--- |
| 1024×768 | 768KB | 1.5MB | 2.3MB | 3.0MB |
| 1280×1024 | 1.3MB | 2.5MB | 3.8MB | 5.0MB |
| 1600×1200 | 1.8MB | 3.7MB | 5.5MB | 7.3MB |

If you’ve examined ads for video cards, no doubt you have noticed that many of these products sport far more RAM than is required even for a huge 1600×1200 pixel display at a high color depth. Cards with 128MB are not uncommon, in fact. Why this discrepancy? The answer is 3D graphics. When handling 3D graphics, the video card takes over much of the task of *rendering* the images—that is, converting raw data such as object sizes, distances, and light sources into 2D images to be displayed on a monitor. These tasks are very computationally intensive. They also require a great deal in the way of RAM to support the computations. The video card must be able to store an assortment of information about objects’ characteristics, intermediate computation results, and so on.

Some video cards can benefit from some extra RAM even when using 2D graphics. These cards can use special memory addressing modes to boost speed slightly, or might be able to store more than one screen of data at a time, which allows you to switch back and forth between screens quite quickly. Some of these functions require special support in your X server, however, and that support might not exist. One common use for extra RAM that is frequently supported is in a *virtual X desktop*. You can configure X so that it displays a desktop larger than your current video mode—for instance, 1024×768 when your monitor is running only 800×600. You can then pan the display so that you see an 800×600-sized portion of the large 1024×768 display. X can use the extra video memory to store the entire 1024×768 display, making the panning operation smoother than it would be if X had to redraw windows and other objects as you pan.

### Tip

> If you’re not using all of your video card’s memory on your current display resolution, you might be tempted to increase the bit depth to get some use from the RAM your card includes. Increasing your color depth unnecessarily slows down video display, however. Also, some programs, such as WordPerfect 8 and Netscape, have problems handling high-color-depth displays, particularly those with 24-bit modes. (32-bit sometimes causes problems, too.) For most users, a 16-bit display is quite adequate. An 8-bit display is usually inadequate, because X is far from frugal in allocating colors. An 8-bit display often runs out of colors very quickly, resulting in poor color options in some programs.

Some video cards support memory expansion, so you can buy a card with a small amount of RAM and expand that RAM at a later date. Unfortunately, RAM for such cards usually comes in proprietary formats, so it can be difficult to purchase RAM from anybody but the card's manufacturer. This results in grossly inflated prices for the RAM, even after the video card has become obsolete.

If you don't plan to make heavy use of OpenGL applications, there's little need to spend extra money on a video card that features huge amounts of RAM. 8MB will probably be plenty for any but the largest displays. If you want to use 3D graphics programs, though, you might want to get 32MB, 64MB, or even more on your video card.

## XFree86

Any decision you make concerning the purchase of a video card is inextricably linked to XFree86. Although there are other X servers for Linux, XFree86 is the one that ships with all Linux distributions, and the alternatives are commercial products. Therefore, relying upon an XFree86 alternative seldom makes economic sense, because it can substantially increase the cost of Linux video support. In most cases, XFree86 is adequate.

## Basic Design of XFree86

Linux's GUI environment is built up of several different layers. Many of the components that comprise each layer can be removed and replaced with equivalent components without disrupting the function of other layers of the system. Examples include

-   **The X server**
    The X server contains what is, in most OSs, called the video driver. The X server can be written for one specific video chipset or family of chipsets (such as the XF86_S3V server for S3's VRGE series chipsets), or it can contain drivers for many unrelated chipsets (such as the XF86_SVGA server). The X server is the most important component of X when it comes to determining video hardware support.
-   **X libraries**
    X programs usually rely upon program libraries, which are routines that are potentially useful to any program of a certain type. XFree86 includes a set of libraries that are required by X programs.
-   **The window manager**
    A window manager controls the appearance of windows on the screen. Different window managers create different-looking drag bars, resizing controls, and so on. Window managers also handle the desktop—the background on which all windows reside. They usually include some means of launching programs from a pop-up menu. As a user, you can choose any of literally dozens of window managers for Linux. You can find out about many of the choices from http://www.p1iq.org/xwinman/.
-   **X utilities**
    XFree86 comes with a large number of small programs that help make X a usable environment. For instance, the xterm program creates a window in which a text-based Linux shell runs, as shown in Figure 12.4.

![](img/860d0c38bd76c9ded976e9d1e179ef25_372_0.png)

### FIGURE 12.4
An xterm window lets you type commands as if you were logged in to Linux using text mode.

-   **A program’s GUI toolkit**
    Unlike the GUI environments of Windows, OS/2, and macOS, X’s GUI environment is quite sparse. Therefore, several $GUI$ toolkits, or widget sets, have emerged. These packages provide tools for programmers to let them easily display and control features such as dialog boxes, menus, and scrollbars. Because the programmer of an application selects the GUI toolkit, this is one of the few features of the Linux GUI that you as an end user can’t modify.
-   **The desktop environment**
    Since the late 1990s, two projects have been underway to develop complete $desktop$ environments for Linux. These environments provide an integrated series of applications, including a window manager, a file manager, help utilities, xterm-like programs, and so on. The goal is to provide a single user-friendly environment with a consistent look and feel. The two projects are the $K$ Desktop Environment (KDE; http://www.kde.org) and the GNU Network Object Model Environment (GNOME; http://www.gnome.org).

Most of these layers of software function independently of the X server and the underlying video hardware you use. You can use any GUI toolkit, window manager, or desktop environment on any video card, for instance, provided the X server supports the video card. Some of these tools make assumptions about the video hardware, however. Specifically, many X programs work best with large display sizes—at least 800×600, and occasionally 1024×768. Using a smaller screen can result in control windows that don’t fit on the display. X’s color allocation model works best when the system has many colors available—16-bit color depth or greater. You can use a less capable display, but you might need to use a virtual desktop that’s larger than your physical screen, or suffer through poor color selections.

## Locating an Appropriate Server

When you install X, or when you install a new video card in an existing system, you must select an appropriate server. In most Linux distributions, each server is shipped in a separate package. For instance, the `XF86_SVGA` server comes in the `XFree86-SVGA-3.3-4.1.1386.rpm` file in Caldera OpenLinux 2.3. This package contains only the `XF86_SVGA` program file and the associated man page.

The list of common video chipsets earlier in this chapter included information on the X servers that support many of these chipsets. For more specific information, you should consult the XFree86 Web page, and specifically the information at http://www.xfree86.org/support. Here you’ll find documentation for specific versions of XFree86. This documentation includes release notes for specific video card chipsets. You can find information here on what server to use for your video card.

In some cases, you might have a choice of using two different XFree86 servers. For instance, many chipsets in the S3 ViRGE family can use either the `XF86_SVGA` server or the `XF86_S3V` server. The former is a multipurpose server that works with many recent chipsets, whereas the latter is specific to the S3 ViRGE series. The more specific server is not necessarily the better one, however. The XFree86 project has been moving development away from separate servers and toward the monolithic `XF86_SVGA` server. This server might contain better acceleration or more features than a chipset-specific server.

As noted earlier, a few chipset manufacturers have developed XFree86 servers for their products. It’s therefore worth checking the board manufacturer’s and the chipset manufacturer’s Web sites for such software. Also, the Linux distributor SuSE actively develops X servers for recently released products. You can find out more at http://www.suse.de/en/support/xserver.

## Configuring XFree86 for Your Video Card

XFree86 configuration is something of a mysterious art. It sometimes proceeds smoothly, but other times results in serious hair pulling. With any luck, Linux will correctly detect and configure your card when you install the OS. If you’re replacing an existing card on an already-installed Linux system, however, or if Linux didn’t correctly identify your card during installation, you must configure XFree86 after installation.

![](img/860d0c38bd76c9ded976e9d1e179ef25_373_0.png)
