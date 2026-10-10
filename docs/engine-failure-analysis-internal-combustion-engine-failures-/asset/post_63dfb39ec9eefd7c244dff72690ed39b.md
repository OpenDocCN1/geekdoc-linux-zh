
## LINUX DESKTOP ENVIRONMENTS (CONT.)

| Name | Description and Download Site |
| :--- | :--- |
| KDE | A desktop environment that relies on the Qt toolkit. Although KDE works with some window managers, it is easiest and best to use the default KDE window manager. Currently offers as many as twice the number of compatible applications as GNOME.<br>Download site: http://www.kde.org. |

At installation, your Linux system was configured to run in one of these interface modes by default. If the system starts in the console mode, you can use startx to start the X Window System.

You can still use the text-only console mode even if you are running the X Window System. To do so, you launch a *terminal emulation program*. Such a program provides a window in which the shell prompt appears. You can then use Linux as if you were working in the console mode. The table that follows provides a list of commonly available terminal emulators.

## LINUX TERMINAL EMULATION UTILITIES

| Name | Description |
| :--- | :--- |
| eterm | VT102 terminal emulator designed to work with the Enlightenment window manager. |
| gnome-terminal | GNOME-compatible implementation of xterm with VT102 compatibility. |
| kterm | Multilingual and color version of xterm. |
| kvt | KDE-compatible implementation of rxvt. |
| rxvt | Color-enabled version of xterm that consumes less memory by deleting Tektronix 4014 compatibility. Can use an XPM graphic as a window background. |
| xterm | Monochrome. Emulates DEC VT102/VT220 and Tektronix 4014 and compatible terminals. |

## Essential Typing and Editing Skills

If you are working in the console mode or in a terminal emulation utility (explained in the previous section), you see the *system prompt*. The system prompt informs you that the shell is running and ready to accept your commands.

On most Linux systems, the *bash* shell is the default for console mode. If your system is running the *bash* shell and you are logged in as an ordinary user, the system prompt is `$`. It is `#` if you're logged in as the root user.

To use your system in console mode, you will type commands. You will find the following editing and control shortcuts helpful. Chapter 3 fully details the keyboard shortcuts you can use with *bash*.

## EDITING AND CONTROL SHORTCUTS

| Use This Keyboard Shortcut | To Do This |
| :--- | :--- |
| Backspace | Delete previous character |
| Ctrl + h | Delete previous character |
| Delete | Delete current character |
| Ctrl + d | Delete current character |
| Ctrl + u | Delete entire line |
| Ctrl + c | Cancel command |
| Ctrl + d | Log out |
| Return | Execute command |
| Enter | Execute command |

## Using Virtual Consoles

Because Linux is a multiuser system, it’s possible to establish more than one user session at the same time. This feature dates back to the time when computers were very expensive. To cut down costs, one computer could be used by several people at once, with each user accessing the system by means of a *remote terminal* (an input-output device featuring a keyboard and display but lacking any data processing or storage capabilities). Although few Linux users implement multiuser systems using remote terminals, you can still make use of the system's capability to run more than one user session at a time. For example, your system is preconfigured to run two or more virtual consoles, which are like separate computers. Your system starts in the default console, which is called the system console. Your system may have been configured with five or more virtual consoles.

To switch to the first virtual console while you are using X, press Ctrl + Alt + F1. To view the second virtual console, press Ctrl + Alt + F2, and so on to view successive virtual consoles. Just how many virtual consoles are available depends on how your system was configured. On Red Hat and Red Hat-derived systems, Ctrl + Alt + F7 returns to the system console. You can also switch virtual consoles using the chvt command.

In most of the consoles, you will see a login prompt. You can log in to one of these consoles and start a separate user session. This capability provides a convenient way to switch from X to the console mode. If you are running X in the default console, you can switch to a virtual console to start a console mode session. Some systems are configured so that you can start a second X session in one of the virtual consoles, but this is not recommended unless your system is equipped with lots of memory (128MB or 256MB).

## The X Window System

The X Window System provides a graphical user interface for Linux systems. Called X for short, the system is divided into two components: the X server, which responds to requests for interface services and controls the display hardware; and X clients, the X-compatible applications that request services from the X server. X servers are designed to work with specific brands and models of hardware, including video adapters, mice, keyboards, and monitors. For Intel-based Linux distributions, the default X server is XFree86 (available for download at http://www.xfree86.org), a series of X servers that are designed to work with popular video adapters and monitors. The following table provides you with some handy XFree86 keyboard shortcuts.

## XFREE86 KEYBOARD SHORTCUTS

| Use This Keyboard Shortcut | To Do This |
| :--- | :--- |
| Ctrl + Alt + Backspace | Kill the X server. **Caution**: You will lose work in any open applications. |
| Ctrl + Alt + Keypad plus | Change to the next video mode specified in the XFree86 configuration file. |
| Ctrl + Alt + Keypad minus | Change to the previous video mode specified in the XFree86 configuration file. |
| Ctrl + Alt + Fn | Switch to the *n*th virtual terminal; for example, Ctrl + Alt + F3 switches to the third virtual terminal. |

Chances are that X is already installed on your system; most Linux distributions use an installation utility that configures X automatically. If not, you can configure X by using the XF86Setup or Xconfigurator utilities discussed in this chapter.

A *window manager* is a special type of X client. It enables you to control the size and position of application windows. Most window managers offer additional features, including some that resemble those of desktop environments. The table that follows lists the most common Linux window managers.

## LINUX WINDOW MANAGERS

| Name | Description and Download Site |
| :--- | :--- |
| AfterStep | A window manager that emulates the NeXT desktop using fvwm code. Its features include application docking, themes, pinnable menus, gradient-rendered window decorations, virtual desktops, GNOME compliance, KDE compliance, and integrated support for GNUStep applications. Download site: http://www.afterstep.org. |

## LINUX WINDOW MANAGERS (CONT.)

| Name | Description and Download Site |
| :--- | :--- |
| Enlightenment | This is the default window manager for current Red Hat Linux and Mandrake distributions. It is highly compatible with GNOME. It includes all the features of Window Maker and AfterStep, plus sound support, TrueType support with anti-aliasing, and advanced graphics features. <br>Download site: http://www.enlightenment.org/. |
| fvwm | Widely available on Linux distributions, this is a highly configurable window manager with advanced features, such as drag-and-drop compatibility, virtual desktops, workspace switchers, and application icons. <br>Download site: http://www.fvwm.org/. |
| fvwm '95 | This is a version of fvwm that is modified to look like Microsoft Windows 95, including the taskbar. <br>Download site: ftp://mitac11.uia.ac.be/html-test/fvwm95.html. |
| IceWM | This is a GNOME-compatible window manager that offers several default themes, including Motif, GTK, OS/2 Warp, and Windows 95. Features include virtual desktops, a taskbar, drag-and-drop, workspace switchers, themes, application icons, and window list menus. <br>Download site: http://icewm.sourceforge.net/. |
| WindowMaker | A window manager that emulates the NeXT desktop, but without using fvwm code. Its features include application docking, themes, pinnable menus, gradient-rendered window decorations, virtual desktops, GNOME compliance, excellent configuration menu system, and integrated support for GNUStep applications. <br>Download site: http://www.windowmaker.org/. |
