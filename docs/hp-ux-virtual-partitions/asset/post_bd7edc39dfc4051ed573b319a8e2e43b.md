
## Motif

Motif consists of the following:

- mwm window manager - Executable program that provides Motif-based window frames, window management, and a workspace menu in the X environment.
- Motif widget toolkit - Higher-level library of widgets and gadgets, the graphical components used to control the user environment.
- Motif style guide - A manual defining the Motif appearance and behavior for programmers.
- Configuration files - The system.mwmrc file containing configuration information for the workspace menu and key and button bindings. Resources for the window manager are in mwm in the /usr/lib/X11/app-defaults directory.

Motif provides the window manager for the end-user, the widget toolkit for application developers, and the style guide to help developers design and build proper Motif-conformant applications. As with X, system administrators can view Motif mostly as “programmer’s stuff,” part of the underlying infrastructure, and focus on developing appropriate CDE configuration files.

## CDE

As we have already seen, CDE consists of the following:

- Workspace Manager - Executable program that provides Motif-based window frames, window management, a workspace menu, and the front panel.
- File Manager - Program that iconically manages files and directories through direct manipulation.
- Style Manager - Container of dialog boxes that control elements of the CDE environment, like workspace color and fonts.
- Help Manager - This program provides context-sensitive help text on CDE components.
- Login Manager - Daemon-like application that handles login and password verification.
- Session Manager - Manager that handles saving and restoring user sessions.
- Application Manager - Manager that registers and keeps track of applications in the CDE environment.
- Configuration Files - A big bunch, most of which you can avoid dealing with (see the next section).

CDE also provides a number of basic, end-user productivity-enhancing applications. In general, CDE provides a graphical environment into which users, or you, their system administrator, can incorporate the software tools needed to do their work.

# X, Motif, and CDE Configuration Files

X, Motif, and CDE all use configuration files to shape their appearance and behavior. Elements of appearance and behavior such as foreground color, keyboard focus policy, and client decoration are resources that can be controlled by values in the appropriate configuration file. In X, Motif, and CDE, the word “resource” has a special meaning. It doesn’t refer to vague natural resources or generic system resources, but to rather specific elements of appearance and behavior. Some examples are the foreground resource, the keyboardFocusPolicy resource, and the clientDecoration resource. For example, the foreground color could be black, keyboard focus policy could be explicit, and client decoration could be plus-title (title bar only). These would appear in some appropriate configuration file as the following:

```
*foreground: black
*keyboardFocusPolicy:explicit
*clientDecoration: +title
```

Which configuration file these resources appear in depends on the scope of the effect desired (system-wide or individual user) and the graphical interface level being used (X, Motif, or CDE).

## X Configuration Files

The X Window System has the following configuration files:

- sys.X11start
- sys.Xdefaults
- system.mwmrc
- X*screens
- X*devices
- X*pointerkey

By convention, these files are located in the /usr/lib/X11 directory; however, I have noticed that many systems have eliminated this directory and moved many of the X-related files elsewhere in the system. In addition, each X client application has its own app-defaults configuration file located, also by convention, in the /usr/lib/X11/app-defaults directory. Although six files are listed above, unless you're configuring a workstation for multiple-display screens (X*screens), multiple-input devices (X*devices), or keyboard-only pointer navigation (X*pointerkey), you'll typically need to work with only sys.x11start, sys.Xdefaults, and system.mwmrc.

The sys.x11start file was a script used to start X and X clients before the advent of CDE. System administrators or knowledgeable users modified sys.x11start so that the appropriate mix of X clients started “automatically.” The sys.Xdefaults file was read as X started to obtain values for various appearance and behavior resources. Modifications to sys.Xdefaults ensured that the X environment and clients had the proper appearance and behavior. system.mwmrc contained the configuration of the Workspace menu and button and key bindings. system.mwmrc has been replaced by the Motif version also, system.mwmrc.

## Motif Configuration Files

Motif added only one new configuration file to the X list: system.mwmrc.

By convention, this file is kept with the X configuration files in /usr/lib/X11. Actually, this file isn’t new; it is the Motif version of system.mwmrc, which simply replaced system.mwmrc in Motif environments.

Whereas X brought network and interclient communication standards to the graphical user interface, Motif brought a standard for appearance and behavior, the standard originally defined in IBM’s System Application Architecture Common User Access (SAACUA), which forms the basis of most PC-based GUIs. Thus, push buttons and scroll bars have a defined look and a defined behavior, and double-clicking always causes the default action to happen.

From a programmer’s point of view, the Motif Widget Toolkit represents quite an advance over programming in “raw” X. From a user’s or system administrator’s point of view, the Motif user environment is about the same as the X environment, except that the mwm Window Manager is replaced with the Motif window manager.

## CDE Configuration Files

It is possible to point to over 80 files that, in one way or another, contribute to configuring some aspect of CDE. By convention, these files reside in the /usr/dt directory. However, if you remove from this list such files as those that:

- Configure CDE applications as opposed to the environment itself
- Establish default actions and datatype definitions that, although you create your own definitions in separate files, you never modify
- Are CDE working files and should not be customized
- Are more appropriately associated with configuring the UNIX, X, and Motif environments underlying CDE, including the various shell environments, that CDE has approximately 19 configuration files, as shown in Table 14-1

### Table 14-1 CDE Configuration Files

| 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 | 11 | 12 | 13 | 14 | 15 | 16 | 17 | 18 | 19 |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| *.Xauthority | *.Xdefaults | *.dprofile | dtwm.fp | dt.wmrc | sys.dprofile | sys.dwmc | sys.font | sys.resources | sys.sessions | Xaccess | Xconfig | Xfailsafe | Xreset | Xresources | Xservers | Xsession | Xsetup | Xstartup |

### Table 14-2 CDE Configuration File Influence

Table 14-2 organizes CDE configuration files according to their content and the breadth of their influence:

| Nature of Configuration File | System-Wide Influence | User's Personal Influence |
|---|---|---|
| Environment Variables | sys.dprofile | .dprofile |
| | Xconfig | |
| | Xsession | |
| Appearance & Behavior Resources | sys.resources | .Xdefaults |
| | Xconfig | |
| | Xresources | |
| | sys.fonts | |

Still, configuring CDE is not something you want to start hacking at without a little preparation and a good idea of what you want to accomplish. All CDE configuration files are pretty well commented, so a good first step is to print the ones you want to modify.

Although 19 configuration files are still a lot, don’t be alarmed by the number. You won’t need to modify many of them, and can ignore a couple that you modify once and then forget. You need to understand in depth for periodic modification only one or two, perhaps a system-wide *.dt file for custom actions and datatypes or maybe dtwm.fp, if you are required to modify the front panel on a regular basis for some reason.
