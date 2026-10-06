
## Chapter 3: Getting Started with the Desktop

- Intel video cards — The Intel i810 and i830 through i945 Intel video cards are supported.
- 3DFX video cards — 3DFX Voodoo3 through Voodoo5 cards should work, but have not been tested. (3DFX was bought by NVIDIA a few years ago.)

Because direct rendering interface (DRI) is required for AIGLX, cards that don't support this feature cannot be used. Support for NVIDIA cards is open development. Although not officially supported, the nouveau Xorg driver is an experimental 3D open source driver for NVIDIA cards with Fedora. Cards that are known to work with AIGLX ATI R 128 and Mach 64, Matrox G200 through G550, and 3DFX Voodoo 1 and 2.

If you have a video card, the next trick in getting AIGLX to work in Fedora is to have the right software packages installed. If you installed the GNOME desktop, you should already have all the packages you need. These packages include compiz (the compiz window manager), glx-utils, gtk2-engines, mesa-libGL, mesa-libGLU, and xorg-x11-dri or xorg-x11-dri-x86 (depending on your video card needs).

If your video card was properly detected and configured, you may be able to turn some of the Desktop Effects to see the effects that have been implemented so far. To turn on Desktop Effects from the GNOME desktop, select SYSTEM -> Preferences -> Look and Feel -> Desktop Effects. When the Desktop Effects pop-up window appears, select Enable Desktop Effects. From the KDE desktop, select the Settings window, select Desktop Effects. Then choose Enable Desktop Effects.

- Stops the current window manager and starts the window manager.
- Enables the Windows Wobble When Moved effect. With this effect on, when you grab the title bar of the window to move it, the window will wobble as it moves. Menus and other items on the desktop also wobble.
- Enables the Workspaces on a Cube effect. Drag a window from the desktop to the right or the left the desktop will rotate like a cube, with each of your workspaces appearing as a side of that cube. Drop the window on the workspace where you want it to go. You can also click on the Workspace Switcher applet in the bottom panel to rotate the cube to different workspaces.

Figure 3-23 shows an example of desktop rotating around a cube.

The following are interesting effects you can get with your 3D AIGLX desktop:

- Spin cube — Hold Ctrl+Alt keys and right and left arrow keys. The desktop cube spins to each successive workspace (forward and back).
- Slowly rotate cube — Hold the Ctrl+Alt keys, and hold the left button, and move the mouse around on the screen. The cube will move slowly with the mouse among the workspaces.

- Tab through windows — Hold the Alt key and press the Tab key. You will see reduced versions of all your windows in a strip in the middle of your screen, with the current window highlighted in the middle. Still holding the Alt key, press Tab or Shift+Tab to move forward and backwards through the windows. Release the keys when the one you want is highlighted.

![](img/63c86e1d25a0e2be7e9f6de6b6f02530_181_0.png)

- Scale and separate windows — If your desktop is cluttered, hold Ctrl+Alt and press the arrow key. Windows will shrink and separate on the desktop. Still holding Ctrl+Alt, use your arrow keys to highlight the window you want and release the keys to have that window come to the surface.

- Scale and separate workspaces — Hold Ctrl+Alt and press the down arrow key to see reduced images of the workspace shown on a strip. Still holding Ctrl+Alt, use right and left keys to move among the different workspaces. Release the keys to the workspace you want is highlighted.

- Send current window to next workspace — Hold Ctrl+Shift+Alt keys and press the left and right arrow keys. The current window will move to the next workspace to the left or right, respectively.

- Slide windows around — Press and hold the mouse button, and then press the left, right, up, or down arrow keys to slide the current window around the screen.

If you tired of wobbling windows and spinning cubes, turning off the AIGLX 3D effects and returning Metacity as the window manager can be quite simple. Just select System -> Preferences -> Look and Feel -> Desktop Effects again and toggle the Enable Desktop Effects to turn off the feat.

If you have a supported video card, but find that you are not able to turn on the Desktop Effects, check that your X server started properly. In particular, make sure that your /etc/X11/xorg.conf file is properly configured. Make sure that glx are loaded by the Module section. Also, add an extension that appears as:

```
Section "extensions"
Option "Composite"
EndSection
```

Another option is to add the following line to the /etc/X11/xorg.conf file in the Device section:

```
Option XANooOffscreenPmaps
```

The XANooOffscreenPmaps option will improve performance.
Check your /var/log/xorg.0 file to make sure that DRI and AIGLX features are started correctly. The messages in that file can help you.

## Using Xfce Desktop

The Xfce desktop provides a lightweight interface. To meet its goals of running quickly, use Xce, here are some examples:

- Thunar — A file manager for the desktop.
- Xfce Settings — A settings manager for the desktop.
- Mousepad — A simple text editor.

Figure 3-24 shows an example of desktop rotating around a cube.

![](img/63c86e1d25a0e2be7e9f6de6b6f02530_181_0.png)

## Troubleshooting Your Desktop

If your desktop is not functioning (or at all) it may be that your video card was not configured. This section helps you get your video card properly.

## GUI doesn't work at start-up

If Fedora or RHEL has been successfully installed (along with the desired desktop environment) but the GUI wasn't set to boot time, you may see only a text-based login prompt. This login prompt may look something like:

```
Fedora release 10
Kernel 2.6.27 on an i86
YourComputer login:
```

Log in as the root user. As noted earlier, you can check if you have a GUI that is at least working enough for you to correct it. Type the following command:

```
# startx
```

## What Happens During Startup?

The X server and graphical login screen is started by the startup script. By default, the login screen is displayed by the GNOME display manager (gdm), which handles logging in and starting the desktop environment for your console, as well as graphical logins from other computers and X terminals.

The startup script is only launched if the run level in the /etc/initabb file is set to 5, as follows:

```
id:5:initdefault:
```

If the initdefault state is 3, the system boots to a text-based login prompt. Chapter 12 for information on Linux run states and startup-processes.

Some processes started during each X session are launched from scripts in the /etc/X11/xinitrc directory. Check those scripts to see if any of the settings might be causing problems. (You can use those scripts to launch applications of each time X starts.)
