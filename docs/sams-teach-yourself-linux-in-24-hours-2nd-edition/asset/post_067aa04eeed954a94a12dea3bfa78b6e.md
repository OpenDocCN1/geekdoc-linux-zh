
Click the Save Now menu item to save your changes (they are put in the files desk and rc.config in the .wmconfig directory in your home directory.)

You can start different X11 clients from the command line of a terminal window or through fvwm's root menu. To use this menu, move your mouse cursor to a blank area of the desktop, click your left mouse button, and scroll down to a desired group of programs, as shown in Figure 7.6.

## FIGURE 7.6

Use fvwm's root menus to launch different X11 clients.

![](img/b5a8a94bdbf7778e1f1f2a5ed6c74e27_175_0.png)

> If you accidentally click the Disable Looking Glass menu item in the root Config menu, you can always start Looking Glass by typing lg in the command line of a terminal window.

The fvwm window manager also supports numerous keyboard commands to control the mouse pointer, menus, and the currently active window. Using these commands, it is possible to control windows or the mouse and select menu items without lifting your fingers from the keyboard. Table 7.2 lists some of the more common commands.

## TABLE 7.2 COMMAND fvwm WINDOW AND POINTER KEYBOARD COMMANDS

| Command | Description |
|---|---|
| Alt+A | Pops up Applications menu |
| Alt+C | Pops up Config menu |
| Alt+D | Pops up Desktop menu |
| Alt+Esc | Displays graphic list of windows |
| Alt+F | Pops up Graphics menu |
| Alt+G | Pops up Games menu |
| Alt+H | Pops up Help menu |
| Alt+I | Pops up Internet Connectivity menu |
| Alt+P | Pops up Productivity Tools menu |
| Alt+R | Pops up Amusement menu |
| Alt+S | Pops up Shells menu |
| Alt+T | Pops up Terminals menu |
| Alt+Tab | Activates next window |
| Alt+V | Pops up Software Development menu |
| Alt+X | Pops up Text and Publishing menu |
| Alt+Y | Pops up System administration menu |
| Ctrl+Alt+down arrow | Moves pointer down 100 pixels |
| Ctrl+Alt+left arrow | Moves pointer left 100 pixels |
| Ctrl+Alt+right arrow | Moves pointer right 100 pixels |
| Ctrl+Alt+up arrow | Moves pointer up 100 pixels |
| Ctrl+down arrow | Moves active window down to next desktop |
| Ctrl+left arrow | Moves active window to next left desktop |
| Ctrl+right arrow | Moves active window to next right desktop |
| Ctrl+up arrow | Moves active window up to next desktop |
| Shift+Alt+Tab | Activates previous window |
| Shift+Ctrl+Alt+down arrow | Moves pointer down 1 percent of screen |
| Shift+Ctrl+Alt+left arrow | Moves pointer left 1 percent of screen |
| Shift+Ctrl+Alt+right arrow | Moves pointer right 1 percent of screen |
| Shift+Ctrl+Alt+up arrow | Moves pointer up 1 percent of screen |

If you like the fvwm window manager, you might also want to try AfterStep, a sophisticated customization of fvwm's configuration files.

## Starting AfterStep

The AfterStep window manager, by Frank Fejes, Alfredo Kenji Kojima, and Dan Weeks, provides window management, controls, and other features similar to the commercial NEXTSTEP operating system (see Figure 7.7). These features include the following:

- 3D, configurable icons
- A "Wharf," or icon dock, for launching X11 clients
- Pop-up, multiple icon menus
- Window shade-type window controls (double-click a window's title bar to draw the shade up or down)
- Sophisticated title bars, buttons, and other decorations
- Styled, pop-up root menus

## FIGURE 7.7

The AfterStep window manager provides sophisticated window controls, icons, and an application "Wharf" for your X sessions.

![](img/b5a8a94bdbf7778e1f1f2a5ed6c74e27_177_0.png)

You can use AfterStep as the default window manager through the Default WM menu item in the root display Config menu. AfterStep uses the same menu and desktop configuration scheme as fvwm, so you can make changes to your desktop and save the settings for future use (changes are reflected in the rc.config file in the .wmconfig directory in your home directory).

## Starting the twm Window Manager

The twm, or Tom's Window Manager, found under the /usr/X11R6/bin directory, is one of the original window managers for the X Window System. The twm client, developed by Tom LaStrange and other authors, provides the most basic window operations, such as window titles, icons, root window menus, and other custom mouse or keyboard commands. Figure 7.8 shows a typical twm window management session.

## FIGURE 7.8

The twm, or Tab window manager, provides basic X11 desktop displays with program lists, icons, and window controls.

![](img/b5a8a94bdbf7778e1f1f2a5ed6c74e27_178_0.png)

Start this window manager, like the others, by clicking the Default WM menu item in the root display Config menu. However, twm does not use the same menu and desktop configuration scheme as the fvwm or AfterStep window managers. If you make twm the default window manager, you can't go back to using any other manager until you edit the .rc.config file in the .wmconfig directory in your home directory! Open this file with your favorite text editor, and look for the WINMGR setting, like this:

```
WINMGR="twm"
```

You can delete this setting or change it to another window manager, like this:

```
WINMGR='afterstep'
```

Save the file, and restart X11 to use the new window manager. The configuration file for the twm window manager, system.twmrc, is found in the /etc/X11/twm directory. If you're the root operator, you can customize this file to support features and programs of your system for all users. If you want to make your own custom twm features, copy this file as .twmrc, and save it in your home directory.

## X11 Terminal Programs

X11 terminal clients provide a console with command-line access to the shell. Although you don't need to use a terminal during your X sessions, it might be a good idea to keep
at least one open (or iconified) so you can start other programs. Having several windows open at one time is also a convenient way to learn new commands because you can have the manual page displayed in one window while you try out the program in another window. You can also use multiple terminal windows to copy and paste information between programs.

This section introduces you to several terminal programs you might want to use with X11: cmdtool, rxvt, xterm, kvt, and kterm. Table 7.3 lists these various terminals.

Table 7.3 X11 Terminal Clients Included with OpenLinux

| Name | Description |
|---|---|
| ansi-xterm | Symbolic link to xterm-color |
| cmdtool | Terminal window emulator included with Sun's OpenWindows |
| color-xterm | Symbolic link to xterm-color |
| kterm | Multilingual terminal emulator |
| kvt | Menu-enabled X11 terminal included with KDE |
| rxvt | Memory efficient, color-capable terminal |
| xterm | Standard X11 terminal included with XFree86 |
| xterm-color | Shell script to run xterm as a color terminal (using the xterm-16color entry in the /etc/termcap database) |

## Changing the xterm Terminal Settings

The xterm client is a color-capable terminal emulator. When started, it displays an open window with a command line. You can run programs, do word processing, or perform nearly any function you normally do when you aren't running X11. Like most X11 terminal emulators, xterm features a resizable window. Depending on the window manager you use, buttons on the window's title bar enable you to move, size, minimize, or maximize the window and might enable you to close or kill the window and any running programs started from the window. If you minimize an xterm window, an icon might appear on the desktop or be placed in an icon dock or taskbar, depending on the window manager.

> **New TERM** If you start xterm from another terminal, you can choose how and where to initially display the new window through the use of command-line options called X11 Toolkit options. These are discussed in the section “Learning X11 Basic Operations” later in this hour. One feature xterm shares with the kvt terminal emulators is the capability to change fonts on-the-fly.

For example, if you want your terminal to use a larger or smaller font, all you have to do is move the cursor inside the terminal window, hold down the Ctrl key, and press the right mouse button. A menu called VT Fonts with a list of sizes pops up from which you can select larger or smaller sizes.

![](img/b5a8a94bdbf7778e1f1f2a5ed6c74e27_180_0.png)

> One really great feature of xterm's VT Fonts menu is the Selection option. Here's how it works: First, run the xterm client, and then start the xfontsel client from the command line. The xfontsel client displays different fonts in many variations, and you can see the effects of different point sizes or orientation on a selected font. After you find an extremely readable font for your display, click the Select button at the top of the xfontsel window. Then, move your mouse cursor to the xterm window, hold down the Ctrl key, press the right mouse button, and select the VT Fonts menu item Selection. Voilà! Your xterm window now uses the font you selected with the xfontsel client. This is handy for finding the best typeface to use for your terminal.

Although nearly all terminals support scrolling, not all terminal emulators have nicely drawn scroll bars. You can control whether scrolling is enabled and scroll bars are visible by holding down the Ctrl key and pressing the middle mouse button (for two-button mouse users, make sure you enable three-button emulation and depress both mouse buttons).

If you don't need all these features or need more memory to run programs, you might want to use the rxvt terminal emulator, discussed next.

## Using the Memory-Efficient rxvt Terminal

The rxvt client, or terminal emulator, is a color-capable X11 console window with fewer, but possibly more useful, features than the xterm client, including the following:

- Smaller size, so this client uses less memory or swap space
- Color-capable terminal emulator
- Supports limited X Toolkit command-line options
- Does not have Tektronix 4014 emulation, which is not really needed for standalone Linux X11 workstations

rxvt supports at least one of the same command-line options as xterm—the -e option to run programs in a standalone X window. The -e option is useful if you want to run
