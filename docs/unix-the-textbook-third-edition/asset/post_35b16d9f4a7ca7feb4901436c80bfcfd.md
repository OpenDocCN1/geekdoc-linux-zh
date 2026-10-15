
# ProgramMenu
# A collection of three useful programs activated with the right-most mouse button
AddToMenu ProgramMenu "Useful Programs" Title
+    "GNU emacs" Exec exec emacs
+    "Dolphin" Exec exec dolphin
+    "FileZilla" Exec exec filezilla

A description of each element of the menu definition is as follows:

After the comments explaining the contents of the menu in brief, any menu definition must begin with a line that has the command AddToMenu. A handle that can be referenced by other menus or components like mouse buttons follows the command; in other words, if you wish to call this menu as a submenu somewhere else in the config file, you would refer to it with the name ProgramMenu. Next, the title Useful Programs, which will appear as text at the top of the menu, is placed on its own line. A plus (+) symbol appears as the first character in each line on which you want a menu choice to appear. Then the title for the menu choice appears on each line, such as Dolphin. The three programs we are adding to this menu, emacs, dolphin, and filezilla, are placed after three Exec exec commands, which follow the entry that will appear in the menu for each. Table 22.3 shows how this menu will appear on screen.

To actually bind this menu to the right-most mouse button, and have it activated when the current position is in the root window, the following lines must appear in the config file where you bind mouse buttons. Notice that the previous binding of the winlist module to this mouse button has been commented out of the file!

```
#Mouse 3    R    A    winlist
Mouse 3    R    A    ProgramMenu
```

# EXERCISE 22.10

Using the preceding menu example as a model, design your own menu activated by the right-most mouse button to launch some of the important applications you run on your system. Name the menu MyApplications. Hint: A program that does not open its own window when it begins to execute will not show anything or launch!

TABLE 22.3 Your Own Pop-Up Menu
Useful Programs
GNU emacs
Dolphin
FileZilla

*FvwmTaskBar: Button Title ATerm, Icon mini/xterm.png, Action (Mouse 1) FvwmATerm

*FvwmTaskBar: Action Click3 Menu FvwmWindowOpsMenu

*FvwmTaskBar: StartIcon mini/fvwm.png

# 22.2.4.9 FvwmPager

FvwmPager is used to show the layout of your virtual desktop. It will show all the pages and desktops you have set up, and the windows opened in each.

Example lines from ~/.fvwm/config:

```
*FvwmPager: Back #908090
*FvwmPager: Fore #484048
##*FvwmPager: Font -adobe-helvetica-bold-r-*-* -10-*-* -*-* -*-*
# turn off desktop names for swallowing in the previous button bar example:
*FvwmPager: Font none
*FvwmPager: Hilight #cab3ca
*FvwmPager: Geometry -1-1
*FvwmPager: Label 0 Misc
*FvwmPager: Label 1 Maker
*FvwmPager: Label 2 Mail
*FvwmPager: Label 3 Matlab
*FvwmPager: SmallFont 5x8
*FvwmPager: Balloons All
*FvwmPager: BalloonBack Yellow
*FvwmPager: BalloonFore Black
*FvwmPager: BalloonFont lucidasanstypewriter-12
*FvwmPager: BalloonYOffset +2
*FvwmPager: BalloonBorderWidth 1
*FvwmPager: BalloonBorderColor Black
```

# 22.2.4.10 FvwmButtons

Buttons and button bars can create freeform panels of any size or shape (including nonrectangular windows). It can swallow other applications, even applications not designed for docking, have "panels" that slide out and consist of other panels, has a "startup notification" feature, hundreds of possible bindings, uses the FVWM Colorsets feature, and can alter dynamically and respond to window manager events.

Example lines from ~/.fvwm/config:

```
############### FvwmButtons button-bar ###############
*FvwmButtons: Geometry 520x100-1-1
*FvwmButtons: Back bisque3
*FvwmButtons: (Frame 2 Padding 2 2 Container(Rows 2 Columns 5 Frame 1 \
Padding 10 0))
```

```
*FvwmButtons: (3x2 Frame 2 Swallow "FvwmIconMan" "Module FvwmIconMan")
*FvwmButtons: (1x2 Frame 2 Swallow(UseOld) "FvwmPager" "Module FvwmPager 0 0")
*FvwmButtons: (1x2 Frame 0 Container(Rows 2 Columns 2 Frame 0))
*FvwmButtons: (Frame 2 Swallow(UseOld,NoHints,Respawn) "xbiff"
'Exec exec xbiff -bg bisque3')
*FvwmButtons: (Frame 3 Swallow(UseOld,NoHints,Respawn) "xclock"
'Exec exec xclock -bg bisque3 -fg black -hd black -hl black -padding 0 -update 1')
*FvwmButtons: (2x1 Frame 2 Swallow(UseOld,NoHints,Respawn) "xload"
'Exec exec xload -bg bisque3 -fg black -update 5 -nolabel')
*FvwmButtons: (End)
*FvwmButtons: (End)
```

For a more detailed description of the options available for customizing FVWM, see the man page for FVWM.

To gain more familiarity with the features and utilities of a nonintegrated GUI installation, go to Problems 1–12 at the end of this chapter.

# 22.3 THE KDE4 DESKTOP MANAGER

The default desktop management system installed with PC-BSD is KDE4.

KDE stands for the K Desktop Environment, and was developed by a volunteer organization of many programmers. The KDE4 desktop manager is an integrated system, in the sense that it provides a consistent and uniform implementation of functions, such as an application programmers interface (API), an object request broker (ORB), window management, desktop configuration tools, session management, and most importantly, application programs. The uniformity of these functions in an integrated system necessarily goes beyond the rudimentary provisions that the X Window System makes for creating and maintaining a graphical interface to UNIX. The drawbacks to this kind of system are its size and complexity, not making it feasible, for example, for installation on an embedded system with limited memory and disk capacity. In the sections that follow, we assume that you have installed PC-BSD as your UNIX system. The default installation method on PC-BSD specifies that the KDE4 desktop manager will start automatically.

If your particular UNIX system does not start KDE4 automatically when the system boots up, but you have installed KDE4 as your default GUI, you can always begin a KDE4 session by typing startx at the UNIX shell prompt after you have logged in. We do not cover the installation of KDE4 as a package on any UNIX system, but leave this as a problem at the end of the chapter.

# 22.3.1 Logging In and Out

After successfully installing and after the first login process to your UNIX system, every subsequent login is done by using a login window, similar to one of the methods shown in
