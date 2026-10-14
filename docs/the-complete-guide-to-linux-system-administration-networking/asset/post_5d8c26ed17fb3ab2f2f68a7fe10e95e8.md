
## Figure 2-3 The Workspace Switcher on the GNOME Panel

![](img/43f64015de86d989e30eff5bb284fb96_95_0.png)

## Table 2-1 GNOME Keyboard Shortcuts

| Keyboard shortcut | Description |
|---|---|
| Alt+Tab | Rotate focus among all windows |
| Ctrl+d | Exit from a command-line window, closing that window |
| PrtSc (Print Screen) | Copy the current screen to the desktop clipboard. You can then use the paste function in most graphical drawing tools to paste the screen image. |
| Alt+Left mouse button | Move the window; with Alt pressed, you can click anywhere in a window and drag it to a new location instead of clicking and dragging using the title bar |
| Alt+Right mouse button | Display the window control menu by clicking anywhere in a window except on its title bar |
| Ctrl+Alt+Backspace | Emergency exit from the X Window System. This immediately returns you to the graphical login prompt or to text mode. If you have any open windows with unsaved documents (such as a text editor), the information in those windows will be lost. |
| Alt+F1 | Display the GNOME main menu |
| Alt+F4 | Close the active window |
| Alt+F5 | Return a maximized window to its previous size |
| Alt+F7 | Move the active window; use the arrow keys to move the window (the current screen location is shown in the middle of the window), then press Enter when you're done moving |
| Alt+F8 | Resize the active window; use the arrow keys to adjust the size (the current size is shown in the middle of the window), then press Enter when you're done resizing |
| Alt+F9 | Minimize the current window |
| Alt+F10 | Maximize the current window |
| F1 | Open a window displaying the online help system |

## CONFIGURING GNOME AND KDE

GNOME and KDE are both highly configurable. In this section you learn about how the desktop configuration utilities are accessed and also explore a few example configuration changes.

### Switching Between Desktop Interfaces

Although the default desktop interface in Red Hat Linux and Fedora is GNOME, many users like to have the option to select which interface they use. You can use the Desktop Switcher utility to select which desktop is displayed when you log in.

To use this utility, you enter the command switchdesk followed by the name of the desktop that you want to switch to (such as GNOME or KDE) in a terminal window. Remember, you can right-click your desktop and choose Open Terminal to open a terminal window. For example, this command changes your default desktop to KDE if you have installed the KDE software packages:

```
$ switchdesk KDE
```

A graphical version of this program called the Desktop Switcher (launched using the switchdesk-gui command) is also available, as shown in Figure 2-4. The corresponding software package is not installed by default, however, so you will need to install that package from your Fedora CDs—as described in Chapter 10, "Managing Software Packages and File Systems"—if you want to experiment with this program instead of using the command line version.

![](img/43f64015de86d989e30eff5bb284fb96_96_0.png)

Figure 2-4 The Desktop Switcher utility, showing available desktop interfaces and window managers on a typical Fedora system

Each user on a Linux system can run the Desktop Switcher or switchdesk independently to select the desktop interface he or she prefers to use. When you select an available desktop in the Desktop Switcher or using switchdesk at the command line, you must exit the X Window System and log in again for the change to take effect. To do this, log out using the last item on the GNOME main menu. When you log in again, the desktop you selected will be running.

> If you experiment with a window manager such as twm, you should plan to use the switchdesk command from a command line to change back to GNOME.

### Saving Your Configuration Between Logins

Each time you log out, GNOME can note which application windows were open so that the next time you log in, the same applications are opened automatically. (But documents within those applications are not automatically loaded.) This is useful when you are working on numerous windows and need to log out for the day. Next time you log in, all of the terminal windows, browsers, and other applications that you opened from within GNOME are opened just as you left them.

To save your configuration between logins, select the Save current setup check box in the message box that appears when you choose Log Out on the GNOME menu. This check box is not selected by default because it takes additional time to log out and log in when application windows must be handled. You can change this setting so that your current setup is saved by default each time you log out. The next section describes how to alter this setting.

### Configuring the Graphical Login Screen

You can set up the graphical login screen according to your preferences using the utilities provided in GNOME. Because the graphical login screen is used by all users on the system, you must be logged in as root or enter the root password before you are permitted to configure most parts of the graphical login screen.

To configure the graphical login screen, you select System Settings, then Login Screen on the GNOME main menu. (You can also run the gdmsetup command from a terminal window.) If you are not logged in as root (you should not typically be logged in as root), you must enter the root password before you can run this utility.

On the General tab of the GDM Setup utility (shown in Figure 2-5), you can select basic options such as whether a user should be logged in automatically as the system boots, or whether to log a user in automatically after a delay that you specify. Your choices depend, of course, on the level of convenience and security that your situation demands. For example, automatically logging in after 10 minutes of sitting idle can be very convenient, but it also presents a large security risk if you regularly leave your system unattended at work.

> Not all of the configuration options for the graphical login prompt are accessible in the GDM Setup utility. You can also change configuration settings by editing the file /etc/X11/gdm/gdm.conf, though this is a fairly advanced operation.

![](img/43f64015de86d989e30eff5bb284fb96_98_0.png)

# Figure 2-5 The GDM Setup utility

On the General tab, you can also select whether to use a standard greeter (login screen) or a graphical greeter for users logging in locally or remotely. Remote login is a powerful feature of the X Window System, but it is not discussed in detail in this book. Chapter 15, “Advanced Topics and Troubleshooting,” contains some additional information. The Security and XDMCP tabs of this utility are also discussed further in Chapter 15, though it is helpful to at least review the Security tab at this point to see what options it offers; several of them may be helpful, such as allowing configuration of the graphical login screen from within the graphical login screen (i.e., before logging in successfully).

Separate tabs configure the standard and graphical greeter screens. The graphical greeter is used by default for local users (users sitting at the computer). On the Graphical greeter tab, you see a list of themes for the graphical login screen. A theme is a collection of colors, fonts, and images that give a display a certain look and feel. You can set up themes for other parts of the desktop interface, as described in the next section. In the Graphical greeter tab, you can select one of the installed themes from the list shown in Figure 2-6, or click the Install new theme button to add a theme to the list that you have downloaded from an Internet site or created yourself.

The face browser feature of the graphical login screen causes it to display a small graphic image for each user. If the theme you select for your graphical greeter includes a face browser, or if the face browser option is selected on the Standard greeter tab (under the Miscellaneous section in the bottom left of the window), then you can configure your own graphical image (your face, or whatever image you choose), by choosing Preferences, then Login Photo on the GNOME main menu.
