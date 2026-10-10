
## Table 8.6 Accessibility Options

| Name | Description |
|---|---|
| Hover Click | Mouse option that triggers a mouse click when the pointer is hovered over an item. |
| Mouse Keys | Mouse option that allows you to use keyboard keys to emulate the mouse functions. |
| Repeat Keys | Keyboard option that modifies how long a key must be pressed down as well as a delay to acknowledge the key repeat. Also called keyboard repeat rate. |
| Screen Keyboard | Keyboard option that displays a visual keyboard on the UI that can be manipulated by a mouse or other pointing device to emulate key strokes. |
| Simulated Secondary Click | Mouse option that sets a primary key to be pressed along with a mouse click to emulate secondary mouse clicks. |
| Slow Keys | Keyboard option that modifies how long a key must be pressed down to acknowledge the key. |
| Sticky Keys | Keyboard option that sets keyboard modifier keys, such as Ctrl and Shift, to maintain their pressed status until a subsequent key is pressed. |

AccessX was a program that provided many of the options in Table 8.6. Thus, you will often see it referred to in the accessibility control panels, such as in the Typing Assist (AccessX) option. One interesting AccessX setting is *Enable By Keyboard*, which allows you to turn on or off accessibility settings via keystrokes on the keyboard.

# Serving Up the GUI

Many players are involved in providing a Linux system user interface. The desktop environment components are only a piece of this puzzle. Figure 8.6 is a rudimentary depiction of serving a GUI to a user.

In Figure 8.6, notice that the window manager is an intermediary in this scenario. A window manager is a program that communicates with the display server (sometimes called a window manager) on behalf of the UI. Each particular desktop environment has its own default window manager, such as Mutter, Kwin, Muffin, Marco, and Metacity.

In the following sections, we will focus on the display server, a program that uses a communication protocol to transmit the desires of the UI to the operating system, and vice versa. The communication protocol is called the display server protocol and can operate over a network.

## Figure 8.6 Serving the GUI components

![](img/c0a399aca0d18f8822d714ad0a173123_313_0.png)

Another member in the display server team is the *compositor*. A compositor program arranges various display elements within a window to create a screen image to be passed back to the client.

> Before computers printed documents, compositors were people. Physical frames (called *chases*) held wooden blocks with letters or images carved on them. A compositor arranged the wooden blocks into the frames to make words and/or images. The compositor handed the frames to the printer, who was also a person. The printer inked the blocks and then pressed the frames onto paper, which resulted in a printed document. A compositor program operates in a similar manner, except it uses multiple elements composed into a single screen image and handed off to the client.

## Figuring Out Wayland

Wayland is a replacement for the X11 display server (described later). It was designed to be simpler, more secure, and easier to develop and maintain. Wayland specifically defines the communication protocol between a display server and its various clients. However, Wayland is also an umbrella term that covers the compositor, the window server, and the display server.

The Wayland protocol was initially released back in 2009, and it is now used by many current Linux desktop environments, such as GNOME Shell and KDE Plasma. If you want to dig down into Wayland, visit its website at `https://wayland.freedesktop.org`.

Exercise 8.1 helps walk you through the display environment in your Linux distribution by using a couple of command-line commands to show the display settings.

## EXERCISE 8.1
### Checking Your Display Server

You can quickly determine what display server your desktop uses, X11 or Wayland, with the following steps:

- 1. Log into your system's GUI. This will start a GUI session for you.
- 2. Open a terminal emulator application.
- 3. Type `echo $WAYLAND_DISPLAY` at the command line and press the **Enter** key. If you get no response and just a command-line prompt back, most likely your system is using X11. If you receive a response, then your desktop environment is probably using Wayland. An additional test will help you ensure what is in use.
- 4. You need to get the GUI session number, so type `loginctl` and press **Enter**. Note the session number.
- 5. Type the command `loginctl show-session session-number -p Type` at the command line, where `session-number` is the number you obtained in the previous step. If you receive `Type=Wayland`, then your desktop environment is using Wayland. If instead you receive `Type=X11`, then your system is using the X11 display server.

The Wayland compositor is Weston, which provides a rather basic desktop experience. It was created as a Wayland compositor reference implementation, which is a compositor requirements example for developers who want to create their own Wayland compositor. Thus, Weston's core focus is correctness and reliability.

Wayland's compositor is swappable. In other words, you can use a different compositor if you need a more full-featured desktop experience. Several compositors are available for use with Wayland, including Arcan, Sway, Lipstick, and Ceyland. However, you may not need to go out and get a Wayland compositor. Many desktop environments create their own Wayland compositors, which are typically embedded within their window manager. For example, Kwin and Mutter both fully handle Wayland compositor tasks.

![](img/c0a399aca0d18f8822d714ad0a173123_314_0.png)

If you have any legacy X11 applications that will not support Wayland, do not despair. The XWayland software is available in the Weston package. XWayland allows X-dependent applications to run on the X server and display via a Wayland session.

If your UI is using Wayland but you are having GUI issues, you can try a few troubleshooting techniques. The following list steps through some basic approaches.

**Try the GUI without Wayland.** If your Linux distribution has multiple flavors of the desktop environment (with Wayland or with X11), log out of your GUI session and pick the desktop environment without Wayland. If your UI problems are resolved, then you know it has most likely something to do with Wayland.

If you do not have multiple flavors of the desktop environment and you are using the GNOME Shell user interface, turn off Wayland. Do this by using super user privileges and editing the `/etc/gdm3/custom.conf` file. Remove the # from the `#WaylandEnable=false` line and save the file. Reboot the system and log into a GUI session and see if the problems are gone.

**Check your system's graphics card.**

If your system seems to be running fine under X11 but gets problematic when using Wayland, check your graphics card. Go to the graphics card vendor's website and see if its drivers support Wayland. Many do, but there are a few famous holdouts that shall go unnamed here.

**Use a different compositor.**

If you are using a desktop environment's built-in compositor or one of the other compositors, try installing and using the Weston compositor package instead. Remember that Weston was built for reliability. If Weston is not in your distribution's software repository, you can get it from `https://github.com/wayland-project/Weston`. This site also contains helpful documentation. If using Weston solves your GUI problem, then you have narrowed down the culprit.

![](img/c0a399aca0d18f8822d714ad0a173123_315_0.png)

Be aware that some desktop environment commands won't work when you have a Wayland session. For example, if you are using GNOME Shell, the `gnome-shell --replace` command will do nothing but generate the message `Window manager warning: Unsupported session type`.

## Examining X11

The X Window System (X for short) has been around since the 1980s, so it has endured the test of time. On Linux the dominant server implementing X was XFree86 until 2004, when a licensing change occurred. This change caused many Linux distributions to switch to the `X.org` foundation's implementation of X.

The `X.org`'s server implements the X Window System version 11. Thus, you will see a wide variety of names about the Linux X display server, such as `X.org-X11`, `X`, `X11`, `X.Org Server`, and so on. We'll use either X or X11 in this chapter.

Currently X11 is being rapidly replaced by Wayland. Not only does Wayland provide better security, but it is far easier to maintain. There are many old and obscure options in the older X11 configuration. However, you still may have distributions using X11, so it is important to understand its basics.

![](img/c0a399aca0d18f8822d714ad0a173123_315_1.png)

If for some reason your X11 session becomes hung, you can quickly kill it off: go back to the display manager screen and log back on to the system. Just press the `Ctrl+Alt+Backspace` key combination. The X11 session will stop and then restart for you, providing the display manager screen so you can log on.
