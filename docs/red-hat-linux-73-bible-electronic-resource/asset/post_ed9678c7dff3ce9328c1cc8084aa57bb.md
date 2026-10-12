
you can have the desktop environment start after you log in (either manually or automatically). Each of these methods is described in this section.

> **CROSS-REFERENCE:** Procedures in this chapter assume that you have already configured your monitor and video driver. If this is not the case, see either Chapter 2 (to configure at installation time) or the “Configuring your Desktop” section earlier in this chapter.

The X Window System GUI (or X GUI) can be started in several different ways, including:

- At boot time — After your video card and monitor are properly configured, you may want to have the X GUI start automatically when Red Hat Linux is booted. You can do this by setting your system initialization state to 5. After you log in, you will see the GNOME or KDE desktop environments.
- From the shell (or starting it yourself) — If you logged in to your computer using a text-based login prompt, you can start the GUI at any time using the `startx` command. When you quit from the GUI, you will be back at your shell prompt.
- At login time — To start with a text-based login screen, but have the X GUI started after you log in, you can add the `startx` command to one of your personal startup files (such as `$HOME/.bash_profile`).

Each of these methods results in the startup of the X GUI and either the GNOME or KDE desktop environment. Along with the GNOME desktop environment, the sawfish window manager (or possibly some other window manager) starts up in order to provide the look-and-feel of the desktop.

> **TIP:** If your X screen ever gets garbled to the point where you don’t know how to exit, or if you want to go to a command-line interface, you can do either by using control keys. From the X GUI, press Ctrl+Alt+F2. You will see a text login. After you log in, you can look for the X process (`ps ax | less`) and kill it (`kill pid`, where `pid` is the X process). Or you can return to the GUI by pressing Ctrl+Alt+F7. These extra screens, referred to as virtual terminals, can be accessed using any function keys from Ctrl+Alt+F2 to Ctrl+Alt+F7.

### Starting the GUI at boot time

After Red Hat Linux boots up, a Red Hat logo and a GNOME (default) or KDE login window appears. You are ready to start using Red Hat Linux from an X Window GUI (probably GNOME and sawfish). Figure 4-1 shows an example of the login window that is used with GNOME:

![](img/1744bde8c889adfab3fc911e1687fecf_147_0.png)

Figure 4-1: Log in to start your desktop environment.

Type your login and password, as prompted, and your personal desktop is displayed.

It is possible to change several important options when you log in using the graphical login screen. In fact, you can even select a desktop environment other than the default. Here are menu options you can select:

- **Session** — From this menu item, you can select the desktop interface that is used with your login session. Besides GNOME, you can possibly choose Default, Failsafe, WindowMaker, or KDE as your interface (depending on which interfaces you have installed).
- **Language** — You can choose from more than a dozen languages to use during your desktop session (all languages are not completely supported).
- **System** — Instead of logging in, you can choose Reboot or Halt from the System selection to restart or halt Red Hat Linux.

The graphical login screen is started by the `prefdm` script, which chooses either the `gdm` (for GNOME) or `kdm` (for KDE) display manager to handle the login screen. These display managers handle both logging in and starting the GUI for your console monitor, as well as graphical logins from other computers and X terminals.

The `prefdm` script is only launched if the run level in the `/etc/inittab` file is set to 5, as follows:

```
id:5:inittab:
```

If the `inittab` state is 3, the system boots to a text-based login prompt.

> **CROSS-REFERENCE:** See Chapter 12 for information on Linux run states and startup processes.

### Starting the GUI yourself

If you log in to a nongraphical interface, you can start your X GUI at any time using the `startx` command. The `startx` command is a shell script that reads your `X` configuration files, and starts the `xinit` command (which starts the `X` server). To run the `startx` command, simply type the following:

```
$ startx
```

> **TIP:** If `startx` fails with a message "Server is already active," it may be that a lock file was not removed the last time X ran. Assuming you are using display 0 (which is the default), type `rm /tmp/.X0-lock`.

If you don't create your own configuration files, `startx` will read several preset configuration files instead. Just as when you log in through the display manager, by default you will see the GNOME desktop environment and the sawfish window manager, and possibly some clients (such as the File Manager and a Help Browser).

To override the default behavior of `startx`, you need to create a `$HOME/.xinitrc` file. The `.xinitrc` file can start up some client processes and run the window manager you choose. Here is an example of the contents of a `$HOME/.xinitrc` file:

```
xeves &
xterm &
xpixmap /usr/share/pixmaps/redhat/shadowman-64.xpm &
exec twm
```

In this example, the `.xinitrc` file tells `startx` to run the `xeyes` and `xterm` clients. Then the `xpixmap` entry sets the background of the root window to lots of little Red Hat icons. Finally, the file starts up the `twm` window manager. Because your `.xinitrc` file overrides the system `xinitrc` file, you may want to add the following line to your `.xinitrc` file to read in other personal X resources (`.Xresources`):

```
xrdb -merge $HOME/.Xresources
```

When you exit your window manager, the X server is halted. You are then returned to your login shell.

### Starting the GUI at login time

If you want to be able to use the X GUI when other users on your system choose not to, set up your user account to start the GUI when you log in. You do this by adding a `startx` command to some personal startup file that only runs once at login time. One place you can add the `startx` command is your `$HOME/.bash_profile` file (assuming you are using the `bash` shell as your login shell).

```
exec startx
```

The default window manager will start immediately after you log in. Then, when you exit the window manager later, you are logged out and returned to the login prompt.

## Using the GNOME Desktop Environment

GNOME (pronounced guh-nome) provides the desktop environment that you get by default when you install Red Hat Linux. This desktop environment provides the software that is between your X Window System framework and the look-and-feel provided by the window manager. GNOME offers a stable and reliable desktop environment, with a few cool features built in.

GNOME is not a window manager, so it must be used with a window manager to provide such things as window borders and window controls. Currently, sawfish is the default window manager with GNOME. You can, however, use other window managers with GNOME that come with Red Hat Linux, including:

- Window Maker
- Twm

You can change to any of these window managers using the GNOME Window Manager window, which you can start from the GNOME menu by choosing Programs $\rightarrow$ Settings $\rightarrow$ Desktop $\rightarrow$ Window Manager. (How to configure GNOME is described later in this section.)

This section describes the GNOME desktop environment and ways of using it. If your Red Hat Linux system is configured to use a GUI by default, you simply need to log in from the graphical login screen. Otherwise, type `startx` from a shell prompt after you log in. In either case, you should see the GNOME desktop environment similar to that shown in Figure 4-2.

![](img/1744bde8c889adfab3fc911e1687fecf_149_0.png)

The GNOME desktop that appears the first time it is started by a new user account includes the GNOME panel, desktop area, desktop icons, and file manager. Descriptions of those elements follow.

The panel contains most of the controls you need to use the desktop. When it first starts, the panel contains buttons for starting applications, a list of active applications, several applets, and a few controls. This is what you should see:

- **Main menu button** (footprint icon) — Click this button to see a list of menu items from which you can select. These menu items include selections for starting applications (such as the Run program window, Lock screen, and Log out selections) and submenus of selections.
  - The Programs menu (under the main menu) includes the following submenus: Applications, Utilities, Games, Graphics, Internet, Multimedia, Settings, and System. There is also a Help selection from this menu.
- **Lock screen** (lock icon) — Lets you lock the screen so it can be reopened using your password only.
- **Start Here** (mushroom icon) — Opens a Start Here window, which is actually a file manager window displaying icons for configuring GNOME.
- **Documentation** (question-mark icon) — Opens the GNOME User’s Guide.
- **Terminal window** (terminal icon) — Opens a Terminal window, which provides access to a Red Hat Linux shell.
- **Mozilla browser** (red monster head logo) — Opens the Mozilla browser window. This software is for browsing the World Wide Web or for running related programs to use e-mail, to compose Web pages, or to view newsgroups. (Mozilla has recently replaced Netscape Navigator as the default browser for Red Hat Linux, though Netscape is still available from the GNOME menu.)
- **Taskbar** — Shows the tasks that are currently running on the desktop. The window that is currently active appears pressed in. Click a task to toggle between opening and minimizing the window.
- **Pager** — This applet shows a tiny view of the multiple desktop areas of your GNOME environment. By default, there are four desktops available. You can change to a different desktop by clicking the area in the pager. Each minidesktop area shows small representations of the active windows within that desk.
  - Click any active application to make it the current application. A sticky application is one that sticks to the same place on the screen, regardless of which desktop you move to. People stick things such as clocks or e-mail notification windows.
- **Clock** — This applet shows the current date and time.

Other useful GNOME controls are located in the following places:
