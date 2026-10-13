
![](img/2c005cbaad58c25c7f54da948131a75e_44_0.png)

FIGURE 3.1 twm managing an X Windows session.

## OTHER WINDOW MANAGERS

Other window managers you might encounter depending on the variation of UNIX you are running include

- olwm—Sun’s default manager for the OpenWindows environment.
- mwm—The Motif window manager. Many commercial window managers are based on, or try to emulate, mwm.
- 4dwm—The default window manager for SGIs running IRIX.
- tvtwm—An experimental extension of twm which includes the capability to set up virtual screens.

There are many other window managers, and a variety will most likely be available to you for use on your machine. After you've investigated your options, you can start building a custom environment that feels and behaves exactly as you want it to.

Remember, it is the window manager that provides user-interface features such as title bars. If you find yourself facing a screen which looks like Figure 3.2 (windows missing title bars, no scroll bars, no icons) it is because there is no window manager running; it either hasn't started for some reason, or it has crashed. You can try starting a window manager by typing twm—if there is a terminal window open that is accepting keyboard input (directing keyboard input to a particular window is also a window manager function). If not, you'll need to exit the X Windows environment and modify your startup files to start the window manager of your choice immediately after starting the X server.

![](img/2c005cbaad58c25c7f54da948131a75e_45_0.png)

Figure 3.2 This X Windows session has lost its window manager.

## Desktop Environments

Historically, window managers have only been used to manage the user's screen. A new type of windowing application is emerging, however. This type functions not only as a window manager in the classical sense, but also provides additional functionality to the user. These desktop environments typically provide sophisticated window management as well as a sort of desktop that is reminiscent of the MS-Windows or Macintosh interface. The desktop frequently includes file management functionality, the capability to create and use icons to launch applications, and an integrated suite of graphical tools for the management and configuration of the computer.

As UNIX vendors try to make their machines more convenient to use, you can expect these desktop environments to become more sophisticated; even today, though, the power and simplicity are quickly approaching that of the popular personal computer interfaces.

Although some of the industry heavy-hitters such as Sun and SGI have weighed in with significant offerings such as OpenWindows and the IRIX desktop, one of the most significant contributions is being made by a non-profit Internet collaborative effort that is developing the freeware product KDE. KDE is a freely-available and downloadable desktop environment that is compatible with a wide range of UNIX implementations.

### KDE

KDE stands for the K Desktop Environment, and—according to the authors—the K stands for nothing. KDE, rather than one of the commercial desktop environments, is discussed here because of its surprising level of sophistication and its portability to such a wide range of platforms.

![](img/2c005cbaad58c25c7f54da948131a75e_46_0.png)

> Compatibility According to the KDE FAQ, KDE is currently known to support Linux, Solaris, FreeBSD, IRIX, and HP-UX, and is expected to be compilable on almost anything which uses the gnu gcc compiler.

KDE provides a sophisticated window manager with convenient extensions such as multiple virtual screens, user-customizable menus, and a facility to automatically remember programs and their placement on the screen between login sessions.

In addition, KDE provides a desktop environment that supports, among other things, icons for files and directories, an application dock, and a quick launch button bar. As you can see in Figure 3.3, the user interface provided by KDE is significantly more user-friendly than the twm (and other typical window manager) interfaces.

![](img/2c005cbaad58c25c7f54da948131a75e_47_0.png)

Figure 3.3 KDE makes X Windows friendly.

Following is a look at some of the KDE window features:

- **KDE Window List**—Shows you a list of all the windows that are currently available, even if they're completely hidden on the screen.
- **Application-Specific Widget**—The leftmost widget on the title bar. Its functions are specific to the application associated with the window.
- **Pushpin Widget**—This button locks the window to your display, making it available on any virtual screen you access.
- **Iconify, Expand, and Destroy Window Buttons**—These buttons give you control of the window; minimize it, maximize it, or close it entirely.
- **KDE Quick-Start Application Icons**—Puts you one click away from your most frequently used programs.
- **KDE Toolbar**—This panel includes pop-up menus to start programs, select windows, and configure your environment, as well as other useful utilities.
- **KDE Environment Setup Utility**—Allows you to control such things as your screen saver, display settings, and so on.
- **KDE Desktop Icons**—These icons which live on your desktop represent files, directories, or applications.

In addition to user interface sophistication, KDE provides an integrated suite of tools for configuring your machine and your user interface, and offers a set of useful point-and-click interfaces to general UNIX programs and utilities. Some of these utilities will be discussed in other lessons; so, if you're using a desktop environment of some sort already, pay attention to these sections to see how KDE—and desktop environments in general—can make your life easier.

If you're looking for a way to make your UNIX experience feel a bit more like your personal computer, look into whether your system administrator can install KDE for you.

## SUMMARY

This lesson taught you about the background of graphical user interfaces, and about the X Window System in particular. Understanding X Windows will enable you to take advantage of these graphic-based tools.

- X Windows is based on a client/server model. The client runs anywhere you want it to and makes display requests. The server runs on the machine with the display screen and attempts to honor those requests.
- The X Window System requires a window manager to implement user-interface conveniences such as title bars.
- X Windows mice can behave in strange ways—if at first you don’t succeed, click and click again.
- X Windows can focus keyboard input to a window in a number of different ways. Pay attention to where your cursor is.
- In the X Windows environment, icons usually represent minimized windows rather than applications.
- The advent of desktop environments is bringing application icons to the world of X Windows.

For all the power of desktop environments, and all the automation of newer window managers, their configurations are usually stored in ugly text files in your home directory. If you want to duplicate your environment from one machine to another, these are a good place to start.

## LESSON 4

### THE FILE SYSTEM

![](img/2c005cbaad58c25c7f54da948131a75e_50_0.png)

*In this lesson you'll learn the basics of the UNIX file system as well as a few convenient tricks to make your UNIX life easier.*

To a beginner, the UNIX file system can appear to be a strange and uninviting place—so many files, and you with just a command line to type at. Bear skin and stone knife time, right? Wrong. Although access to the UNIX file system might initially appear cryptic and primitive, UNIX provides extremely sophisticated file access and control. This sophistication is born of many simple commands from which more complicated commands can be constructed.

### FILE SYSTEM DESIGN

Before even the simple commands will make sense, you need to understand a few things about the design of the UNIX file system. Although this might not seem like a very important part of the user experience, the UNIX file system is a bit different than the personal computer file systems you might be familiar with. Actually, you will probably find the biggest differences to be to your liking.

*UNIX file systems have a single root directory.* Unlike Macintosh file systems with their multiple drive icons on the desktop or Windows file systems with their ABCs, the UNIX file system has a single top-level directory—the *root* directory. UNIX considers its files to be arranged in what is essentially a tree shape, with the root directory as the base, or root. UNIX's tree, however, is upside down as compared to normal trees. The root directory can contain files and other directories, the second-level directories can contain more files and more directories, and so on.
