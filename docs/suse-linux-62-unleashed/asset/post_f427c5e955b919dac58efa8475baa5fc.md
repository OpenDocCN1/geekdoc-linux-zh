
change the look of your desktop, its color scheme, or its handling of windows. For details other about ways to configure AfterStep, read its FAQ or browse to http://www.afterstep.org.

## The fwm Window Manager

The fwm window manager (shown in Figure 5.3) is a descendant of the twm window manager but has several advantages, such as using less memory, supporting fancier window decorations, and providing virtual desktops.

**Figure 5.3**
The fwm window manager is an improvement over
The XII's twm window manager.

![](img/cbac72550c7126a22162e94d91a0c360_144_0.png)

You'll find fwm default file under the /usr/X11/lib/X11/fwm directory which is named system.fwmrc. Copy this file to your home directory as .fwmrc and make changes to customize it for your use. fwm startup file contains sections for customizing window colors and style, menus, and the number of virtual desktops. Look for the desktop section, which looks like the following:

```
# Set up the virtual desktop and pager
#set the desktop top size in units of physical screen size
DesktopSize 3x2
```

fwm's startup file defines different virtual desktops. You can move to a different desktop by pressing your left button on the appropriate square in the desktop pager's window. By changing the DesktopSize value you can either reduce or increase the number of virtual desktops. For example, a setting like the following to add another desktops:

DesktopSize 4x2

When you restart fwm, you'll see that two additional desktops have been added to the fwm pager. If you do not use an X11 display manager to log into KDE Linux, you can use fwm for your X11 session using the word in your start line:

```
startx fwm
```

## The fvwm Window Manager

fvvwm window manager (see Figure 5.4) is a configurable taskbar, window frames, buttons, scrollbars, and capability for extensive customization.

**Figure 5.4**
fvwm window manager provides many sophisticated window controls.

![](img/cbac72550c7126a22162e94d91a0c360_145_0.png)

This window manager's default startup file is found under /usr/X11R/lib/fvwm directory as system.fvwmrc. Copy this file to your home directory as .fvwmrc and make changes to customize your X11 sessions. If you do not use an X11 display manager to log in, insert fvwm in your start command line:

```
startx fvwm
```

fvwm features virtual desktops, a desktop pager, and window decorations. You can also use this window manager (like fwm) without an X11 pointing device. Table 5.1 lists nearly two dozen keyboard commands you can use to manipulate or move over windows.

### Table 5.1 Common Fvwm Keyboard Commands

| Command | Keyboard Command |
| :--- | :--- |
| Close current window | Alt+F9 |
| Display list of windows | Alt+F2 |
| Iconify current window | Alt+F4 |
| Jump to next window | Alt+F1 |
| Move current window | Alt+F5 |
| Next desktop down | Shift+Alt+down |
| Next desktop to left | Shift+Alt+left |
| Next desktop to right | Shift+Alt+right |
| Next desktop up | Shift+Alt+up |
| Pointer down 100 pixels | Shift+Ctrl+down |
| Pointer down 5 pixels | Shift+down |
| Pointer left 100 pixels | Shift+Ctrl+left |
| Pointer left 5 pixels | Shift+left |
| Pointer right 100 pixels | Shift+Ctrl+right |
| Pointer right 5 pixels | Shift+right |
| Pointer up 100 pixels | Shift+Ctrl+up |
| Pointer up 5 pixels | Shift+up |
| Resize current window | Alt+F6 |
| Toggle Maximize/normal window size | Shift+Alt+F3 |
| Toggle sticky window in desktops | Shift+Alt+F4 |

> Note To be able to use your keyboard properly during your X11 sessions, make sure you've configured X with the correct keyboard setting for your computer. See Chapter 4 for details about the XFConfig file.

## Features of the icew Window Manager

The icew window manager (in Figure 5.5) is designed to look like OS/2 or Windows 95 (and other window managers). It features numerous mouse and keyboard commands, and its configuration files and directories are located under /usr/X11R/lib/X11/icew manager. To start an X session window manager, type start icew at the command line and press Enter.

```
start icew
```

Figure 5.5 The icew desktop features an easy-to-use, if not minimalistic, X11 environment.

![](img/cbac72550c7126a22162e94d91a0c360_147_0.png)

## Features of the K Desktop Environment

KDE supports many of the features you'd expect in a modern desktop environment, including those commonly found in commercial software libraries, such as Motif, and the Common Desktop Environment or CDE (which is now only offered by one vendor, Xi-Graphics, for Linux). These features include:

- A suite of personal productivity tools, such as disk and network utilities, designed to use the desktop interface and the capability to import and export data to other tools
- Session management, so open applications and window positions are remembered between sessions
- "Sticky Buttons” to put an application or window on every desktop
- Network Transparent Access, or NTA, so you can click or drag and drop a graphic document’s icon in an FTP window to display or transfer the graphic
- Pop-up menus and built-in help for nearly any desktop action and KDE client
- A desktop trash can for safer file deletions
- Graphic configuration of your system’s desktop, keyboard, mouse, and sound
- Programs and other data represented as icons on the desktop or in windows with folder icons
- Drag-and-drop actions (such as copy, link, move, and delete) for files

## Introduction and Installation SuSE Linux

The fwm window manager (shown in Figure 5.3) is a descendant of the twm window manager but has several advantages, such as using less memory, supporting fancier window decorations, and providing virtual desktops.

**Figure 5.3**
The fwm window manager is an improvement over
The XII's twm window manager.

![](img/cbac72550c7126a22162e94d91a0c360_144_0.png)

You'll find fwm default file under the /usr/X11/lib/X11/fwm directory which is named system.fwmrc. Copy this file to your home directory as .fwmrc and make changes to customize it for your use. fwm startup file contains sections for customizing window colors and style, menus, and the number of virtual desktops. Look for the desktop section, which looks like the following:

```
# Set up the virtual desktop and pager
#set the desktop top size in units of physical screen size
DesktopSize 3x2
```

fwm's startup file defines different virtual desktops. You can move to a different desktop by pressing your left button on the appropriate square in the desktop pager's window. By changing the DesktopSize value you can either reduce or increase the number of virtual desktops. For example, a setting like the following to add another desktops:

DesktopSize 4x2

When you restart fwm, you'll see that two additional desktops have been added to the fwm pager. If you do not use an X11 display manager to log into KDE Linux, you can use fwm for your X11 session using the word in your start line:

```
startx fwm
```

## The fvwm Window Manager

fvvwm window manager (see Figure 5.4) is a configurable taskbar, window frames, buttons, scrollbars, and capability for extensive customization.

**Figure 5.4**
fvwm window manager provides many sophisticated window controls.

![](img/cbac72550c7126a22162e94d91a0c360_145_0.png)

This window manager's default startup file is found under /usr/X11R/lib/fvwm directory as system.fvwmrc. Copy this file to your home directory as .fvwmrc and make changes to customize your X11 sessions. If you do not use an X11 display manager to log in, insert fvwm in your start command line:

```
startx fvwm
```

fvwm features virtual desktops, a desktop pager, and window decorations. You can also use this window manager (like fwm) without an X11 pointing device. Table 5.1 lists nearly two dozen keyboard commands you can use to manipulate or move over windows.

### Table 5.1 Common Fvwm Keyboard Commands

| Command | Keyboard Command |
| :--- | :--- |
| Close current window | Alt+F9 |
| Display list of windows | Alt+F2 |
| Iconify current window | Alt+F4 |
| Jump to next window | Alt+F1 |
| Move current window | Alt+F5 |
| Next desktop down | Shift+Alt+down |
| Next desktop to left | Shift+Alt+left |
| Next desktop to right | Shift+Alt+right |
| Next desktop up | Shift+Alt+up |
| Pointer down 100 pixels | Shift+Ctrl+down |
| Pointer down 5 pixels | Shift+down |
| Pointer left 100 pixels | Shift+Ctrl+left |
| Pointer left 5 pixels | Shift+left |
| Pointer right 100 pixels | Shift+Ctrl+right |
| Pointer right 5 pixels | Shift+right |
| Pointer up 100 pixels | Shift+Ctrl+up |
| Pointer up 5 pixels | Shift+up |
| Resize current window | Alt+F6 |
| Toggle Maximize/normal window size | Shift+Alt+F3 |
| Toggle sticky window in desktops | Shift+Alt+F4 |

> Note To be able to use your keyboard properly during your X11 sessions, make sure you've configured X with the correct keyboard setting for your computer. See Chapter 4 for details about the XFConfig file.

## Features of the icew Window Manager

The icew window manager (in Figure 5.5) is designed to look like OS/2 or Windows 95 (and other window managers). It features numerous mouse and keyboard commands, and its configuration files and directories are located under /usr/X11R/lib/X11/icew manager. To start an X session window manager, type start icew at the command line and press Enter.

```
start icew
```

Figure 5.5 The icew desktop features an easy-to-use, if not minimalistic, X11 environment.

![](img/cbac72550c7126a22162e94d91a0c360_147_0.png)

## Features of the K Desktop Environment

KDE supports many of the features you'd expect in a modern desktop environment, including those commonly found in commercial software libraries, such as Motif, and the Common Desktop Environment or CDE (which is now only offered by one vendor, Xi-Graphics, for Linux). These features include:

- A suite of personal productivity tools, such as disk and network utilities, designed to use the desktop interface and the capability to import and export data to other tools
- Session management, so open applications and window positions are remembered between sessions
- "Sticky Buttons” to put an application or window on every desktop
- Network Transparent Access, or NTA, so you can click or drag and drop a graphic document’s icon in an FTP window to display or transfer the graphic
- Pop-up menus and built-in help for nearly any desktop action and KDE client
- A desktop trash can for safer file deletions
- Graphic configuration of your system’s desktop, keyboard, mouse, and sound
- Programs and other data represented as icons on the desktop or in windows with folder icons
- Drag-and-drop actions (such as copy, link, move, and delete) for files

## Introduction and Installation SuSE Linux

The fwm window manager (shown in Figure 5.3) is a descendant of the twm window manager but has several advantages, such as using less memory, supporting fancier window decorations, and providing virtual desktops.

**Figure 5.3**
The fwm window manager is an improvement over
The XII's twm window manager.

![](img/cbac72550c7126a22162e94d91a0c360_144_0.png)

You'll find fwm default file under the /usr/X11/lib/X11/fwm directory which is named system.fwmrc. Copy this file to your home directory as .fwmrc and make changes to customize it for your use. fwm startup file contains sections for customizing window colors and style, menus, and the number of virtual desktops. Look for the desktop section, which looks like the following:

```
# Set up the virtual desktop and pager
#set the desktop top size in units of physical screen size
DesktopSize 3x2
```

fwm's startup file defines different virtual desktops. You can move to a different desktop by pressing your left button on the appropriate square in the desktop pager's window. By changing the DesktopSize value you can either reduce or increase the number of virtual desktops. For example, a setting like the following to add another desktops:

DesktopSize 4x2

When you restart fwm, you'll see that two additional desktops have been added to the fwm pager. If you do not use an X11 display manager to log into KDE Linux, you can use fwm for your X11 session using the word in your start line:

```
startx fwm
```

## The fvwm Window Manager

fvvwm window manager (see Figure 5.4) is a configurable taskbar, window frames, buttons, scrollbars, and capability for extensive customization.

**Figure 5.4**
fvwm window manager provides many sophisticated window controls.

![](img/cbac72550c7126a22162e94d91a0c360_145_0.png)

This window manager's default startup file is found under /usr/X11R/lib/fvwm directory as system.fvwmrc. Copy this file to your home directory as .fvwmrc and make changes to customize your X11 sessions. If you do not use an X11 display manager to log in, insert fvwm in your start command line:

```
startx fvwm
```

fvwm features virtual desktops, a desktop pager, and window decorations. You can also use this window manager (like fwm) without an X11 pointing device. Table 5.1 lists nearly two dozen keyboard commands you can use to manipulate or move over windows.

### Table 5.1 Common Fvwm Keyboard Commands

| Command | Keyboard Command |
| :--- | :--- |
| Close current window | Alt+F9 |
| Display list of windows | Alt+F2 |
| Iconify current window | Alt+F4 |
| Jump to next window | Alt+F1 |
| Move current window | Alt+F5 |
| Next desktop down | Shift+Alt+down |
| Next desktop to left | Shift+Alt+left |
| Next desktop to right | Shift+Alt+right |
| Next desktop up | Shift+Alt+up |
| Pointer down 100 pixels | Shift+Ctrl+down |
| Pointer down 5 pixels | Shift+down |
| Pointer left 100 pixels | Shift+Ctrl+left |
| Pointer left 5 pixels | Shift+left |
| Pointer right 100 pixels | Shift+Ctrl+right |
| Pointer right 5 pixels | Shift+right |
| Pointer up 100 pixels | Shift+Ctrl+up |
| Pointer up 5 pixels | Shift+up |
| Resize current window | Alt+F6 |
| Toggle Maximize/normal window size | Shift+Alt+F3 |
| Toggle sticky window in desktops | Shift+Alt+F4 |

> Note To be able to use your keyboard properly during your X11 sessions, make sure you've configured X with the correct keyboard setting for your computer. See Chapter 4 for details about the XFConfig file.

## Features of the icew Window Manager

The icew window manager (in Figure 5.5) is designed to look like OS/2 or Windows 95 (and other window managers). It features numerous mouse and keyboard commands, and its configuration files and directories are located under /usr/X11R/lib/X11/icew manager. To start an X session window manager, type start icew at the command line and press Enter.

```
start icew
```

Figure 5.5 The icew desktop features an easy-to-use, if not minimalistic, X11 environment.

![](img/cbac72550c7126a22162e94d91a0c360_147_0.png)

## Features of the K Desktop Environment

KDE supports many of the features you'd expect in a modern desktop environment, including those commonly found in commercial software libraries, such as Motif, and the Common Desktop Environment or CDE (which is now only offered by one vendor, Xi-Graphics, for Linux). These features include:

- A suite of personal productivity tools, such as disk and network utilities, designed to use the desktop interface and the capability to import and export data to other tools
- Session management, so open applications and window positions are remembered between sessions
- "Sticky Buttons” to put an application or window on every desktop
- Network Transparent Access, or NTA, so you can click or drag and drop a graphic document’s icon in an FTP window to display or transfer the graphic
- Pop-up menus and built-in help for nearly any desktop action and KDE client
- A desktop trash can for safer file deletions
- Graphic configuration of your system’s desktop, keyboard, mouse, and sound
- Programs and other data represented as icons on the desktop or in windows with folder icons
- Drag-and-drop actions (such as copy, link, move, and delete) for files

## Introduction and Installation SuSE Linux

The fwm window manager (shown in Figure 5.3) is a descendant of the twm window manager but has several advantages, such as using less memory, supporting fancier window decorations, and providing virtual desktops.

**Figure 5.3**
The fwm window manager is an improvement over
The XII's twm window manager.

![](img/cbac72550c7126a22162e94d91a0c360_144_0.png)

You'll find fwm default file under the /usr/X11/lib/X11/fwm directory which is named system.fwmrc. Copy this file to your home directory as .fwmrc and make changes to customize it for your use. fwm startup file contains sections for customizing window colors and style, menus, and the number of virtual desktops. Look for the desktop section, which looks like the following:

```
# Set up the virtual desktop and pager
#set the desktop top size in units of physical screen size
DesktopSize 3x2
```

fwm's startup file defines different virtual desktops. You can move to a different desktop by pressing your left button on the appropriate square in the desktop pager's window. By changing the DesktopSize value you can either reduce or increase the number of virtual desktops. For example, a setting like the following to add another desktops:

DesktopSize 4x2

When you restart fwm, you'll see that two additional desktops have been added to the fwm pager. If you do not use an X11 display manager to log into KDE Linux, you can use fwm for your X11 session using the word in your start line:

```
startx fwm
```

## The fvwm Window Manager

fvvwm window manager (see Figure 5.4) is a configurable taskbar, window frames, buttons, scrollbars, and capability for extensive customization.

**Figure 5.4**
fvwm window manager provides many sophisticated window controls.

![](img/cbac72550c7126a22162e94d91a0c360_145_0.png)

This window manager's default startup file is found under /usr/X11R/lib/fvwm directory as system.fvwmrc. Copy this file to your home directory as .fvwmrc and make changes to customize your X11 sessions. If you do not use an X11 display manager to log in, insert fvwm in your start command line:

```
startx fvwm
```

fvwm features virtual desktops, a desktop pager, and window decorations. You can also use this window manager (like fwm) without an X11 pointing device. Table 5.1 lists nearly two dozen keyboard commands you can use to manipulate or move over windows.

### Table 5.1 Common Fvwm Keyboard Commands

| Command | Keyboard Command |
| :--- | :--- |
| Close current window | Alt+F9 |
| Display list of windows | Alt+F2 |
| Iconify current window | Alt+F4 |
| Jump to next window | Alt+F1 |
| Move current window | Alt+F5 |
| Next desktop down | Shift+Alt+down |
| Next desktop to left | Shift+Alt+left |
| Next desktop to right | Shift+Alt+right |
| Next desktop up | Shift+Alt+up |
| Pointer down 100 pixels | Shift+Ctrl+down |
| Pointer down 5 pixels | Shift+down |
| Pointer left 100 pixels | Shift+Ctrl+left |
| Pointer left 5 pixels | Shift+left |
| Pointer right 100 pixels | Shift+Ctrl+right |
| Pointer right 5 pixels | Shift+right |
| Pointer up 100 pixels | Shift+Ctrl+up |
| Pointer up 5 pixels | Shift+up |
| Resize current window | Alt+F6 |
| Toggle Maximize/normal window size | Shift+Alt+F3 |
| Toggle sticky window in desktops | Shift+Alt+F4 |

> Note To be able to use your keyboard properly during your X11 sessions, make sure you've configured X with the correct keyboard setting for your computer. See Chapter 4 for details about the XFConfig file.

## Features of the icew Window Manager

The icew window manager (in Figure 5.5) is designed to look like OS/2 or Windows 95 (and other window managers). It features numerous mouse and keyboard commands, and its configuration files and directories are located under /usr/X11R/lib/X11/icew manager. To start an X session window manager, type start icew at the command line and press Enter.

```
start icew
```

Figure 5.5 The icew desktop features an easy-to-use, if not minimalistic, X11 environment.

![](img/cbac72550c7126a22162e94d91a0c360_147_0.png)

## Features of the K Desktop Environment

KDE supports many of the features you'd expect in a modern desktop environment, including those commonly found in commercial software libraries, such as Motif, and the Common Desktop Environment or CDE (which is now only offered by one vendor, Xi-Graphics, for Linux). These features include:

- A suite of personal productivity tools, such as disk and network utilities, designed to use the desktop interface and the capability to import and export data to other tools
- Session management, so open applications and window positions are remembered between sessions
- "Sticky Buttons” to put an application or window on every desktop
- Network Transparent Access, or NTA, so you can click or drag and drop a graphic document’s icon in an FTP window to display or transfer the graphic
- Pop-up menus and built-in help for nearly any desktop action and KDE client
- A desktop trash can for safer file deletions
- Graphic configuration of your system’s desktop, keyboard, mouse, and sound
- Programs and other data represented as icons on the desktop or in windows with folder icons
- Drag-and-drop actions (such as copy, link, move, and delete) for files

## Introduction and Installation SuSE Linux

The fwm window manager (shown in Figure 5.3) is a descendant of the twm window manager but has several advantages, such as using less memory, supporting fancier window decorations, and providing virtual desktops.

**Figure 5.3**
The fwm window manager is an improvement over
The XII's twm window manager.

![](img/cbac72550c7126a22162e94d91a0c360_144_0.png)

You'll find fwm default file under the /usr/X11/lib/X11/fwm directory which is named system.fwmrc. Copy this file to your home directory as .fwmrc and make changes to customize it for your use. fwm startup file contains sections for customizing window colors and style, menus, and the number of virtual desktops. Look for the desktop section, which looks like the following:

```
# Set up the virtual desktop and pager
#set the desktop top size in units of physical screen size
DesktopSize 3x2
```

fwm's startup file defines different virtual desktops. You can move to a different desktop by pressing your left button on the appropriate square in the desktop pager's window. By changing the DesktopSize value you can either reduce or increase the number of virtual desktops. For example, a setting like the following to add another desktops:

DesktopSize 4x2

When you restart fwm, you'll see that two additional desktops have been added to the fwm pager. If you do not use an X11 display manager to log into KDE Linux, you can use fwm for your X11 session using the word in your start line:

```
startx fwm
```

## The fvwm Window Manager

fvvwm window manager (see Figure 5.4) is a configurable taskbar, window frames, buttons, scrollbars, and capability for extensive customization.

**Figure 5.4**
fvwm window manager provides many sophisticated window controls.

![](img/cbac72550c7126a22162e94d91a0c360_145_0.png)

This window manager's default startup file is found under /usr/X11R/lib/fvwm directory as system.fvwmrc. Copy this file to your home directory as .fvwmrc and make changes to customize your X11 sessions. If you do not use an X11 display manager to log in, insert fvwm in your start command line:

```
startx fvwm
```

fvwm features virtual desktops, a desktop pager, and window decorations. You can also use this window manager (like fwm) without an X11 pointing device. Table 5.1 lists nearly two dozen keyboard commands you can use to manipulate or move over windows.

### Table 5.1 Common Fvwm Keyboard Commands

| Command | Keyboard Command |
| :--- | :--- |
| Close current window | Alt+F9 |
| Display list of windows | Alt+F2 |
| Iconify current window | Alt+F4 |
| Jump to next window | Alt+F1 |
| Move current window | Alt+F5 |
| Next desktop down | Shift+Alt+down |
| Next desktop to left | Shift+Alt+left |
| Next desktop to right | Shift+Alt+right |
| Next desktop up | Shift+Alt+up |
| Pointer down 100 pixels | Shift+Ctrl+down |
| Pointer down 5 pixels | Shift+down |
| Pointer left 100 pixels | Shift+Ctrl+left |
| Pointer left 5 pixels | Shift+left |
| Pointer right 100 pixels | Shift+Ctrl+right |
| Pointer right 5 pixels | Shift+right |
| Pointer up 100 pixels | Shift+Ctrl+up |
| Pointer up 5 pixels | Shift+up |
| Resize current window | Alt+F6 |
| Toggle Maximize/normal window size | Shift+Alt+F3 |
| Toggle sticky window in desktops | Shift+Alt+F4 |

> Note To be able to use your keyboard properly during your X11 sessions, make sure you've configured X with the correct keyboard setting for your computer. See Chapter 4 for details about the XFConfig file.

## Features of the icew Window Manager

The icew window manager (in Figure 5.5) is designed to look like OS/2 or Windows 95 (and other window managers). It features numerous mouse and keyboard commands, and its configuration files and directories are located under /usr/X11R/lib/X11/icew manager. To start an X session window manager, type start icew at the command line and press Enter.

```
start icew
```

Figure 5.5 The icew desktop features an easy-to-use, if not minimalistic, X11 environment.

![](img/cbac72550c7126a22162e94d91a0c360_147_0.png)

## Features of the K Desktop Environment

KDE supports many of the features you'd expect in a modern desktop environment, including those commonly found in commercial software libraries, such as Motif, and the Common Desktop Environment or CDE (which is now only offered by one vendor, Xi-Graphics, for Linux). These features include:

- A suite of personal productivity tools, such as disk and network utilities, designed to use the desktop interface and the capability to import and export data to other tools
- Session management, so open applications and window positions are remembered between sessions
- "Sticky Buttons” to put an application or window on every desktop
- Network Transparent Access, or NTA, so you can click or drag and drop a graphic document’s icon in an FTP window to display or transfer the graphic
- Pop-up menus and built-in help for nearly any desktop action and KDE client
- A desktop trash can for safer file deletions
- Graphic configuration of your system’s desktop, keyboard, mouse, and sound
- Programs and other data represented as icons on the desktop or in windows with folder icons
- Drag-and-drop actions (such as copy, link, move, and delete) for files

## Introduction and Installation SuSE Linux

The fwm window manager (shown in Figure 5.3) is a descendant of the twm window manager but has several advantages, such as using less memory, supporting fancier window decorations, and providing virtual desktops.

**Figure 5.3**
The fwm window manager is an improvement over
The XII's twm window manager.

![](img/cbac72550c7126a22162e94d91a0c360_144_0.png)

You'll find fwm default file under the /usr/X11/lib/X11/fwm directory which is named system.fwmrc. Copy this file to your home directory as .fwmrc and make changes to customize it for your use. fwm startup file contains sections for customizing window colors and style, menus, and the number of virtual desktops. Look for the desktop section, which looks like the following:

```
# Set up the virtual desktop and pager
#set the desktop top size in units of physical screen size
DesktopSize 3x2
```

fwm's startup file defines different virtual desktops. You can move to a different desktop by pressing your left button on the appropriate square in the desktop pager's window. By changing the DesktopSize value you can either reduce or increase the number of virtual desktops. For example, a setting like the following to add another desktops:

DesktopSize 4x2

When you restart fwm, you'll see that two additional desktops have been added to the fwm pager. If you do not use an X11 display manager to log into KDE Linux, you can use fwm for your X11 session using the word in your start line:

```
startx fwm
```

## The fvwm Window Manager

fvvwm window manager (see Figure 5.4) is a configurable taskbar, window frames, buttons, scrollbars, and capability for extensive customization.

**Figure 5.4**
fvwm window manager provides many sophisticated window controls.

![](img/cbac72550c7126a22162e94d91a0c360_145_0.png)

This window manager's default startup file is found under /usr/X11R/lib/fvwm directory as system.fvwmrc. Copy this file to your home directory as .fvwmrc and make changes to customize your X11 sessions. If you do not use an X11 display manager to log in, insert fvwm in your start command line:

```
startx fvwm
```

fvwm features virtual desktops, a desktop pager, and window decorations. You can also use this window manager (like fwm) without an X11 pointing device. Table 5.1 lists nearly two dozen keyboard commands you can use to manipulate or move over windows.

### Table 5.1 Common Fvwm Keyboard Commands

| Command | Keyboard Command |
| :--- | :--- |
| Close current window | Alt+F9 |
| Display list of windows | Alt+F2 |
| Iconify current window | Alt+F4 |
| Jump to next window | Alt+F1 |
| Move current window | Alt+F5 |
| Next desktop down | Shift+Alt+down |
| Next desktop to left | Shift+Alt+left |
| Next desktop to right | Shift+Alt+right |
| Next desktop up | Shift+Alt+up |
| Pointer down 100 pixels | Shift+Ctrl+down |
| Pointer down 5 pixels | Shift+down |
| Pointer left 100 pixels | Shift+Ctrl+left |
| Pointer left 5 pixels | Shift+left |
| Pointer right 100 pixels | Shift+Ctrl+right |
| Pointer right 5 pixels | Shift+right |
| Pointer up 100 pixels | Shift+Ctrl+up |
| Pointer up 5 pixels | Shift+up |
| Resize current window | Alt+F6 |
| Toggle Maximize/normal window size | Shift+Alt+F3 |
| Toggle sticky window in desktops | Shift+Alt+F4 |

> Note To be able to use your keyboard properly during your X11 sessions, make sure you've configured X with the correct keyboard setting for your computer. See Chapter 4 for details about the XFConfig file.

## Features of the icew Window Manager

The icew window manager (in Figure 5.5) is designed to look like OS/2 or Windows 95 (and other window managers). It features numerous mouse and keyboard commands, and its configuration files and directories are located under /usr/X11R/lib/X11/icew manager. To start an X session window manager, type start icew at the command line and press Enter.

```
start icew
```

Figure 5.5 The icew desktop features an easy-to-use, if not minimalistic, X11 environment.

![](img/cbac72550c7126a22162e94d91a0c360_147_0.png)

## Features of the K Desktop Environment

KDE supports many of the features you'd expect in a modern desktop environment, including those commonly found in commercial software libraries, such as Motif, and the Common Desktop Environment or CDE (which is now only offered by one vendor, Xi-Graphics, for Linux). These features include:

- A suite of personal productivity tools, such as disk and network utilities, designed to use the desktop interface and the capability to import and export data to other tools
- Session management, so open applications and window positions are remembered between sessions
- "Sticky Buttons” to put an application or window on every desktop
- Network Transparent Access, or NTA, so you can click or drag and drop a graphic document’s icon in an FTP window to display or transfer the graphic
- Pop-up menus and built-in help for nearly any desktop action and KDE client
- A desktop trash can for safer file deletions
- Graphic configuration of your system’s desktop, keyboard, mouse, and sound
- Programs and other data represented as icons on the desktop or in windows with folder icons
- Drag-and-drop actions (such as copy, link, move, and delete) for files

## Introduction and Installation SuSE Linux

The fwm window manager (shown in Figure 5.3) is a descendant of the twm window manager but has several advantages, such as using less memory, supporting fancier window decorations, and providing virtual desktops.

**Figure 5.3**
The fwm window manager is an improvement over
The XII's twm window manager.

![](img/cbac72550c7126a22162e94d91a0c360_144_0.png)

You'll find fwm default file under the /usr/X11/lib/X11/fwm directory which is named system.fwmrc. Copy this file to your home directory as .fwmrc and make changes to customize it for your use. fwm startup file contains sections for customizing window colors and style, menus, and the number of virtual desktops. Look for the desktop section, which looks like the following:

```
# Set up the virtual desktop and pager
#set the desktop top size in units of physical screen size
DesktopSize 3x2
```

fwm's startup file defines different virtual desktops. You can move to a different desktop by pressing your left button on the appropriate square in the desktop pager's window. By changing the DesktopSize value you can either reduce or increase the number of virtual desktops. For example, a setting like the following to add another desktops:

DesktopSize 4x2

When you restart fwm, you'll see that two additional desktops have been added to the fwm pager. If you do not use an X11 display manager to log into KDE Linux, you can use fwm for your X11 session using the word in your start line:

```
startx fwm
```

## The fvwm Window Manager

fvvwm window manager (see Figure 5.4) is a configurable taskbar, window frames, buttons, scrollbars, and capability for extensive customization.

**Figure 5.4**
fvwm window manager provides many sophisticated window controls.

![](img/cbac72550c7126a22162e94d91a0c360_145_0.png)

This window manager's default startup file is found under /usr/X11R/lib/fvwm directory as system.fvwmrc. Copy this file to your home directory as .fvwmrc and make changes to customize your X11 sessions. If you do not use an X11 display manager to log in, insert fvwm in your start command line:

```
startx fvwm
```

fvwm features virtual desktops, a desktop pager, and window decorations. You can also use this window manager (like fwm) without an X11 pointing device. Table 5.1 lists nearly two dozen keyboard commands you can use to manipulate or move over windows.

### Table 5.1 Common Fvwm Keyboard Commands

| Command | Keyboard Command |
| :--- | :--- |
| Close current window | Alt+F9 |
| Display list of windows | Alt+F2 |
| Iconify current window | Alt+F4 |
| Jump to next window | Alt+F1 |
| Move current window | Alt+F5 |
| Next desktop down | Shift+Alt+down |
| Next desktop to left | Shift+Alt+left |
| Next desktop to right | Shift+Alt+right |
| Next desktop up | Shift+Alt+up |
| Pointer down 100 pixels | Shift+Ctrl+down |
| Pointer down 5 pixels | Shift+down |
| Pointer left 100 pixels | Shift+Ctrl+left |
| Pointer left 5 pixels | Shift+left |
| Pointer right 100 pixels | Shift+Ctrl+right |
| Pointer right 5 pixels | Shift+right |
| Pointer up 100 pixels | Shift+Ctrl+up |
| Pointer up 5 pixels | Shift+up |
| Resize current window | Alt+F6 |
| Toggle Maximize/normal window size | Shift+Alt+F3 |
| Toggle sticky window in desktops | Shift+Alt+F4 |

> Note To be able to use your keyboard properly during your X11 sessions, make sure you've configured X with the correct keyboard setting for your computer. See Chapter 4 for details about the XFConfig file.

## Features of the icew Window Manager

The icew window manager (in Figure 5.5) is designed to look like OS/2 or Windows 95 (and other window managers). It features numerous mouse and keyboard commands, and its configuration files and directories are located under /usr/X11R/lib/X11/icew manager. To start an X session window manager, type start icew at the command line and press Enter.

```
start icew
```

Figure 5.5 The icew desktop features an easy-to-use, if not minimalistic, X11 environment.

![](img/cbac72550c7126a22162e94d91a0c360_147_0.png)

## Features of the K Desktop Environment

KDE supports many of the features you'd expect in a modern desktop environment, including those commonly found in commercial software libraries, such as Motif, and the Common Desktop Environment or CDE (which is now only offered by one vendor, Xi-Graphics, for Linux). These features include:

- A suite of personal productivity tools, such as disk and network utilities, designed to use the desktop interface and the capability to import and export data to other tools
- Session management, so open applications and window positions are remembered between sessions
- "Sticky Buttons” to put an application or window on every desktop
- Network Transparent Access, or NTA, so you can click or drag and drop a graphic document’s icon in an FTP window to display or transfer the graphic
- Pop-up menus and built-in help for nearly any desktop action and KDE client
- A desktop trash can for safer file deletions
- Graphic configuration of your system’s desktop, keyboard, mouse, and sound
- Programs and other data represented as icons on the desktop or in windows with folder icons
- Drag-and-drop actions (such as copy, link, move, and delete) for files

## Introduction and Installation SuSE Linux

The fwm window manager (shown in Figure 5.3) is a descendant of the twm window manager but has several advantages, such as using less memory, supporting fancier window decorations, and providing virtual desktops.

**Figure 5.3**
The fwm window manager is an improvement over
The XII's twm window manager.

![](img/cbac72550c7126a22162e94d91a0c360_144_0.png)

You'll find fwm default file under the /usr/X11/lib/X11/fwm directory which is named system.fwmrc. Copy this file to your home directory as .fwmrc and make changes to customize it for your use. fwm startup file contains sections for customizing window colors and style, menus, and the number of virtual desktops. Look for the desktop section, which looks like the following:

```
# Set up the virtual desktop and pager
#set the desktop top size in units of physical screen size
DesktopSize 3x2
```

fwm's startup file defines different virtual desktops. You can move to a different desktop by pressing your left button on the appropriate square in the desktop pager's window. By changing the DesktopSize value you can either reduce or increase the number of virtual desktops. For example, a setting like the following to add another desktops:

DesktopSize 4x2

When you restart fwm, you'll see that two additional desktops have been added to the fwm pager. If you do not use an X11 display manager to log into KDE Linux, you can use fwm for your X11 session using the word in your start line:

```
startx fwm
```

## The fvwm Window Manager

fvvwm window manager (see Figure 5.4) is a configurable taskbar, window frames, buttons, scrollbars, and capability for extensive customization.

**Figure 5.4**
fvwm window manager provides many sophisticated window controls.

![](img/cbac72550c7126a22162e94d91a0c360_145_0.png)

This window manager's default startup file is found under /usr/X11R/lib/fvwm directory as system.fvwmrc. Copy this file to your home directory as .fvwmrc and make changes to customize your X11 sessions. If you do not use an X11 display manager to log in, insert fvwm in your start command line:

```
startx fvwm
```

fvwm features virtual desktops, a desktop pager, and window decorations. You can also use this window manager (like fwm) without an X11 pointing device. Table 5.1 lists nearly two dozen keyboard commands you can use to manipulate or move over windows.

### Table 5.1 Common Fvwm Keyboard Commands

| Command | Keyboard Command |
| :--- | :--- |
| Close current window | Alt+F9 |
| Display list of windows | Alt+F2 |
| Iconify current window | Alt+F4 |
| Jump to next window | Alt+F1 |
| Move current window | Alt+F5 |
| Next desktop down | Shift+Alt+down |
| Next desktop to left | Shift+Alt+left |
| Next desktop to right | Shift+Alt+right |
| Next desktop up | Shift+Alt+up |
| Pointer down 100 pixels | Shift+Ctrl+down |
| Pointer down 5 pixels | Shift+down |
| Pointer left 100 pixels | Shift+Ctrl+left |
| Pointer left 5 pixels | Shift+left |
| Pointer right 100 pixels | Shift+Ctrl+right |
| Pointer right 5 pixels | Shift+right |
| Pointer up 100 pixels | Shift+Ctrl+up |
| Pointer up 5 pixels | Shift+up |
| Resize current window | Alt+F6 |
| Toggle Maximize/normal window size | Shift+Alt+F3 |
| Toggle sticky window in desktops | Shift+Alt+F4 |

> Note To be able to use your keyboard properly during your X11 sessions, make sure you've configured X with the correct keyboard setting for your computer. See Chapter 4 for details about the XFConfig file.

## Features of the icew Window Manager

The icew window manager (in Figure 5.5) is designed to look like OS/2 or Windows 95 (and other window managers). It features numerous mouse and keyboard commands, and its configuration files and directories are located under /usr/X11R/lib/X11/icew manager. To start an X session window manager, type start icew at the command line and press Enter.

```
start icew
```

Figure 5.5 The icew desktop features an easy-to-use, if not minimalistic, X11 environment.

![](img/cbac72550c7126a22162e94d91a0c360_147_0.png)

## Features of the K Desktop Environment

KDE supports many of the features you'd expect in a modern desktop environment, including those commonly found in commercial software libraries, such as Motif, and the Common Desktop Environment or CDE (which is now only offered by one vendor, Xi-Graphics, for Linux). These features include:

- A suite of personal productivity tools, such as disk and network utilities, designed to use the desktop interface and the capability to import and export data to other tools
- Session management, so open applications and window positions are remembered between sessions
- "Sticky Buttons” to put an application or window on every desktop
- Network Transparent Access, or NTA, so you can click or drag and drop a graphic document’s icon in an FTP window to display or transfer the graphic
- Pop-up menus and built-in help for nearly any desktop action and KDE client
- A desktop trash can for safer file deletions
- Graphic configuration of your system’s desktop, keyboard, mouse, and sound
- Programs and other data represented as icons on the desktop or in windows with folder icons
- Drag-and-drop actions (such as copy, link, move, and delete) for files

## Introduction and Installation SuSE Linux

The fwm window manager (shown in Figure 5.3) is a descendant of the twm window manager but has several advantages, such as using less memory, supporting fancier window decorations, and providing virtual desktops.

**Figure 5.3**
The fwm window manager is an improvement over
The XII's twm window manager.

![](img/cbac72550c7126a22162e94d91a0c360_144_0.png)

You'll find fwm default file under the /usr/X11/lib/X11/fwm directory which is named system.fwmrc. Copy this file to your home directory as .fwmrc and make changes to customize it for your use. fwm startup file contains sections for customizing window colors and style, menus, and the number of virtual desktops. Look for the desktop section, which looks like the following:

```
# Set up the virtual desktop and pager
#set the desktop top size in units of physical screen size
DesktopSize 3x2
```

fwm's startup file defines different virtual desktops. You can move to a different desktop by pressing your left button on the appropriate square in the desktop pager's window. By changing the DesktopSize value you can either reduce or increase the number of virtual desktops. For example, a setting like the following to add another desktops:

DesktopSize 4x2

When you restart fwm, you'll see that two additional desktops have been added to the fwm pager. If you do not use an X11 display manager to log into KDE Linux, you can use fwm for your X11 session using the word in your start line:

```
startx fwm
```

## The fvwm Window Manager

fvvwm window manager (see Figure 5.4) is a configurable taskbar, window frames, buttons, scrollbars, and capability for extensive customization.

**Figure 5.4**
fvwm window manager provides many sophisticated window controls.

![](img/cbac72550c7126a22162e94d91a0c360_145_0.png)

This window manager's default startup file is found under /usr/X11R/lib/fvwm directory as system.fvwmrc. Copy this file to your home directory as .fvwmrc and make changes to customize your X11 sessions. If you do not use an X11 display manager to log in, insert fvwm in your start command line:

```
startx fvwm
```

fvwm features virtual desktops, a desktop pager, and window decorations. You can also use this window manager (like fwm) without an X11 pointing device. Table 5.1 lists nearly two dozen keyboard commands you can use to manipulate or move over windows.

### Table 5.1 Common Fvwm Keyboard Commands

| Command | Keyboard Command |
| :--- | :--- |
| Close current window | Alt+F9 |
| Display list of windows | Alt+F2 |
| Iconify current window | Alt+F4 |
| Jump to next window | Alt+F1 |
| Move current window | Alt+F5 |
| Next desktop down | Shift+Alt+down |
| Next desktop to left | Shift+Alt+left |
| Next desktop to right | Shift+Alt+right |
| Next desktop up | Shift+Alt+up |
| Pointer down 100 pixels | Shift+Ctrl+down |
| Pointer down 5 pixels | Shift+down |
| Pointer left 100 pixels | Shift+Ctrl+left |
| Pointer left 5 pixels | Shift+left |
| Pointer right 100 pixels | Shift+Ctrl+right |
| Pointer right 5 pixels | Shift+right |
| Pointer up 100 pixels | Shift+Ctrl+up |
| Pointer up 5 pixels | Shift+up |
| Resize current window | Alt+F6 |
| Toggle Maximize/normal window size | Shift+Alt+F3 |
| Toggle sticky window in desktops | Shift+Alt+F4 |

> Note To be able to use your keyboard properly during your X11 sessions, make sure you've configured X with the correct keyboard setting for your computer. See Chapter 4 for details about the XFConfig file.

## Features of the icew Window Manager

The icew window manager (in Figure 5.5) is designed to look like OS/2 or Windows 95 (and other window managers). It features numerous mouse and keyboard commands, and its configuration files and directories are located under /usr/X11R/lib/X11/icew manager. To start an X session window manager, type start icew at the command line and press Enter.

```
start icew
```

Figure 5.5 The icew desktop features an easy-to-use, if not minimalistic, X11 environment.

![](img/cbac72550c7126a22162e94d91a0c360_147_0.png)

## Features of the K Desktop Environment

KDE supports many of the features you'd expect in a modern desktop environment, including those commonly found in commercial software libraries, such as Motif, and the Common Desktop Environment or CDE (which is now only offered by one vendor, Xi-Graphics, for Linux). These features include:

- A suite of personal productivity tools, such as disk and network utilities, designed to use the desktop interface and the capability to import and export data to other tools
- Session management, so open applications and window positions are remembered between sessions
- "Sticky Buttons” to put an application or window on every desktop
- Network Transparent Access, or NTA, so you can click or drag and drop a graphic document’s icon in an FTP window to display or transfer the graphic
- Pop-up menus and built-in help for nearly any desktop action and KDE client
- A desktop trash can for safer file deletions
- Graphic configuration of your system’s desktop, keyboard, mouse, and sound
- Programs and other data represented as icons on the desktop or in windows with folder icons
- Drag-and-drop actions (such as copy, link, move, and delete) for files

## Introduction and Installation SuSE Linux

The fwm window manager (shown in Figure 5.3) is a descendant of the twm window manager but has several advantages, such as using less memory, supporting fancier window decorations, and providing virtual desktops.

**Figure 5.3**
The fwm window manager is an improvement over
The XII's twm window manager.

![](img/cbac72550c7126a22162e94d91a0c360_144_0.png)

You'll find fwm default file under the /usr/X11/lib/X11/fwm directory which is named system.fwmrc. Copy this file to your home directory as .fwmrc and make changes to customize it for your use. fwm startup file contains sections for customizing window colors and style, menus, and the number of virtual desktops. Look for the desktop section, which looks like the following:

```
# Set up the virtual desktop and pager
#set the desktop top size in units of physical screen size
DesktopSize 3x2
```

fwm's startup file defines different virtual desktops. You can move to a different desktop by pressing your left button on the appropriate square in the desktop pager's window. By changing the DesktopSize value you can either reduce or increase the number of virtual desktops. For example, a setting like the following to add another desktops:

DesktopSize 4x2

When you restart fwm, you'll see that two additional desktops have been added to the fwm pager. If you do not use an X11 display manager to log into KDE Linux, you can use fwm for your X11 session using the word in your start line:

```
startx fwm
```

## The fvwm Window Manager

fvvwm window manager (see Figure 5.4) is a configurable taskbar, window frames, buttons, scrollbars, and capability for extensive customization.

**Figure 5.4**
fvwm window manager provides many sophisticated window controls.

![](img/cbac72550c7126a22162e94d91a0c360_145_0.png)

This window manager's default startup file is found under /usr/X11R/lib/fvwm directory as system.fvwmrc. Copy this file to your home directory as .fvwmrc and make changes to customize your X11 sessions. If you do not use an X11 display manager to log in, insert fvwm in your start command line:

```
startx fvwm
```

fvwm features virtual desktops, a desktop pager, and window decorations. You can also use this window manager (like fwm) without an X11 pointing device. Table 5.1 lists nearly two dozen keyboard commands you can use to manipulate or move over windows.

### Table 5.1 Common Fvwm Keyboard Commands

| Command | Keyboard Command |
| :--- | :--- |
| Close current window | Alt+F9 |
| Display list of windows | Alt+F2 |
| Iconify current window | Alt+F4 |
| Jump to next window | Alt+F1 |
| Move current window | Alt+F5 |
| Next desktop down | Shift+Alt+down |
| Next desktop to left | Shift+Alt+left |
| Next desktop to right | Shift+Alt+right |
| Next desktop up | Shift+Alt+up |
| Pointer down 100 pixels | Shift+Ctrl+down |
| Pointer down 5 pixels | Shift+down |
| Pointer left 100 pixels | Shift+Ctrl+left |
| Pointer left 5 pixels | Shift+left |
| Pointer right 100 pixels | Shift+Ctrl+right |
| Pointer right 5 pixels | Shift+right |
| Pointer up 100 pixels | Shift+Ctrl+up |
| Pointer up 5 pixels | Shift+up |
| Resize current window | Alt+F6 |
| Toggle Maximize/normal window size | Shift+Alt+F3 |
| Toggle sticky window in desktops | Shift+Alt+F4 |

> Note To be able to use your keyboard properly during your X11 sessions, make sure you've configured X with the correct keyboard setting for your computer. See Chapter 4 for details about the XFConfig file.

## Features of the icew Window Manager

The icew window manager (in Figure 5.5) is designed to look like OS/2 or Windows 95 (and other window managers). It features numerous mouse and keyboard commands, and its configuration files and directories are located under /usr/X11R/lib/X11/icew manager. To start an X session window manager, type start icew at the command line and press Enter.

```
start icew
```

Figure 5.5 The icew desktop features an easy-to-use, if not minimalistic, X11 environment.

![](img/cbac72550c7126a22162e94d91a0c360_147_0.png)

## Features of the K Desktop Environment

KDE supports many of the features you'd expect in a modern desktop environment, including those commonly found in commercial software libraries, such as Motif, and the Common Desktop Environment or CDE (which is now only offered by one vendor, Xi-Graphics, for Linux). These features include:

- A suite of personal productivity tools, such as disk and network utilities, designed to use the desktop interface and the capability to import and export data to other tools
- Session management, so open applications and window positions are remembered between sessions
- "Sticky Buttons” to put an application or window on every desktop
- Network Transparent Access, or NTA, so you can click or drag and drop a graphic document’s icon in an FTP window to display or transfer the graphic
- Pop-up menus and built-in help for nearly any desktop action and KDE client
- A desktop trash can for safer file deletions
- Graphic configuration of your system’s desktop, keyboard, mouse, and sound
- Programs and other data represented as icons on the desktop or in windows with folder icons
- Drag-and-drop actions (such as copy, link, move, and delete) for files

## Introduction and Installation SuSE Linux

The fwm window manager (shown in Figure 5.3) is a descendant of the twm window manager but has several advantages, such as using less memory, supporting fancier window decorations, and providing virtual desktops.

**Figure 5.3**
The fwm window manager is an improvement over
The XII's twm window manager.

![](img/cbac72550c7126a22162e94d91a0c360_144_0.png)

You'll find fwm default file under the /usr/X11/lib/X11/fwm directory which is named system.fwmrc. Copy this file to your home directory as .fwmrc and make changes to customize it for your use. fwm startup file contains sections for customizing window colors and style, menus, and the number of virtual desktops. Look for the desktop section, which looks like the following:

```
# Set up the virtual desktop and pager
#set the desktop top size in units of physical screen size
DesktopSize 3x2
```

fwm's startup file defines different virtual desktops. You can move to a different desktop by pressing your left button on the appropriate square in the desktop pager's window. By changing the DesktopSize value you can either reduce or increase the number of virtual desktops. For example, a setting like the following to add another desktops:

DesktopSize 4x2

When you restart fwm, you'll see that two additional desktops have been added to the fwm pager. If you do not use an X11 display manager to log into KDE Linux, you can use fwm for your X11 session using the word in your start line:

```
startx fwm
```

## The fvwm Window Manager

fvvwm window manager (see Figure 5.4) is a configurable taskbar, window frames, buttons, scrollbars, and capability for extensive customization.

**Figure 5.4**
fvwm window manager provides many sophisticated window controls.

![](img/cbac72550c7126a22162e94d91a0c360_145_0.png)

This window manager's default startup file is found under /usr/X11R/lib/fvwm directory as system.fvwmrc. Copy this file to your home directory as .fvwmrc and make changes to customize your X11 sessions. If you do not use an X11 display manager to log in, insert fvwm in your start command line:

```
startx fvwm
```

fvwm features virtual desktops, a desktop pager, and window decorations. You can also use this window manager (like fwm) without an X11 pointing device. Table 5.1 lists nearly two dozen keyboard commands you can use to manipulate or move over windows.

### Table 5.1 Common Fvwm Keyboard Commands

| Command | Keyboard Command |
| :--- | :--- |
| Close current window | Alt+F9 |
| Display list of windows | Alt+F2 |
| Iconify current window | Alt+F4 |
| Jump to next window | Alt+F1 |
| Move current window | Alt+F5 |
| Next desktop down | Shift+Alt+down |
| Next desktop to left | Shift+Alt+left |
| Next desktop to right | Shift+Alt+right |
| Next desktop up | Shift+Alt+up |
| Pointer down 100 pixels | Shift+Ctrl+down |
| Pointer down 5 pixels | Shift+down |
| Pointer left 100 pixels | Shift+Ctrl+left |
| Pointer left 5 pixels | Shift+left |
| Pointer right 100 pixels | Shift+Ctrl+right |
| Pointer right 5 pixels | Shift+right |
| Pointer up 100 pixels | Shift+Ctrl+up |
| Pointer up 5 pixels | Shift+up |
| Resize current window | Alt+F6 |
| Toggle Maximize/normal window size | Shift+Alt+F3 |
| Toggle sticky window in desktops | Shift+Alt+F4 |

> Note To be able to use your keyboard properly during your X11 sessions, make sure you've configured X with the correct keyboard setting for your computer. See Chapter 4 for details about the XFConfig file.

## Features of the icew Window Manager

The icew window manager (in Figure 5.5) is designed to look like OS/2 or Windows 95 (and other window managers). It features numerous mouse and keyboard commands, and its configuration files and directories are located under /usr/X11R/lib/X11/icew manager. To start an X session window manager, type start icew at the command line and press Enter.

```
start icew
```

Figure 5.5 The icew desktop features an easy-to-use, if not minimalistic, X11 environment.

![](img/cbac72550c7126a22162e94d91a0c360_147_0.png)

## Features of the K Desktop Environment

KDE supports many of the features you'd expect in a modern desktop environment, including those commonly found in commercial software libraries, such as Motif, and the Common Desktop Environment or CDE (which is now only offered by one vendor, Xi-Graphics, for Linux). These features include:

- A suite of personal productivity tools, such as disk and network utilities, designed to use the desktop interface and the capability to import and export data to other tools
- Session management, so open applications and window positions are remembered between sessions
- "Sticky Buttons” to put an application or window on every desktop
- Network Transparent Access, or NTA, so you can click or drag and drop a graphic document’s icon in an FTP window to display or transfer the graphic
- Pop-up menus and built-in help for nearly any desktop action and KDE client
- A desktop trash can for safer file deletions
- Graphic configuration of your system’s desktop, keyboard, mouse, and sound
- Programs and other data represented as icons on the desktop or in windows with folder icons
- Drag-and-drop actions (such as copy, link, move, and delete) for files

## Introduction and Installation SuSE Linux

The fwm window manager (shown in Figure 5.3) is a descendant of the twm window manager but has several advantages, such as using less memory, supporting fancier window decorations, and providing virtual desktops.

**Figure 5.3**
The fwm window manager is an improvement over
The XII's twm window manager.

![](img/cbac72550c7126a22162e94d91a0c360_144_0.png)

You'll find fwm default file under the /usr/X11/lib/X11/fwm directory which is named system.fwmrc. Copy this file to your home directory as .fwmrc and make changes to customize it for your use. fwm startup file contains sections for customizing window colors and style, menus, and the number of virtual desktops. Look for the desktop section, which looks like the following:

```
# Set up the virtual desktop and pager
#set the desktop top size in units of physical screen size
DesktopSize 3x2
```

fwm's startup file defines different virtual desktops. You can move to a different desktop by pressing your left button on the appropriate square in the desktop pager's window. By changing the DesktopSize value you can either reduce or increase the number of virtual desktops. For example, a setting like the following to add another desktops:

DesktopSize 4x2

When you restart fwm, you'll see that two additional desktops have been added to the fwm pager. If you do not use an X11 display manager to log into KDE Linux, you can use fwm for your X11 session using the word in your start line:

```
startx fwm
```

## The fvwm Window Manager

fvvwm window manager (see Figure 5.4) is a configurable taskbar, window frames, buttons, scrollbars, and capability for extensive customization.

**Figure 5.4**
fvwm window manager provides many sophisticated window controls.

![](img/cbac72550c7126a22162e94d91a0c360_145_0.png)

This window manager's default startup file is found under /usr/X11R/lib/fvwm directory as system.fvwmrc. Copy this file to your home directory as .fvwmrc and make changes to customize your X11 sessions. If you do not use an X11 display manager to log in, insert fvwm in your start command line:

```
startx fvwm
```

fvwm features virtual desktops, a desktop pager, and window decorations. You can also use this window manager (like fwm) without an X11 pointing device. Table 5.1 lists nearly two dozen keyboard commands you can use to manipulate or move over windows.

### Table 5.1 Common Fvwm Keyboard Commands

| Command | Keyboard Command |
| :--- | :--- |
| Close current window | Alt+F9 |
| Display list of windows | Alt+F2 |
| Iconify current window | Alt+F4 |
| Jump to next window | Alt+F1 |
| Move current window | Alt+F5 |
| Next desktop down | Shift+Alt+down |
| Next desktop to left | Shift+Alt+left |
| Next desktop to right | Shift+Alt+right |
| Next desktop up | Shift+Alt+up |
| Pointer down 100 pixels | Shift+Ctrl+down |
| Pointer down 5 pixels | Shift+down |
| Pointer left 100 pixels | Shift+Ctrl+left |
| Pointer left 5 pixels | Shift+left |
| Pointer right 100 pixels | Shift+Ctrl+right |
| Pointer right 5 pixels | Shift+right |
| Pointer up 100 pixels | Shift+Ctrl+up |
| Pointer up 5 pixels | Shift+up |
| Resize current window | Alt+F6 |
| Toggle Maximize/normal window size | Shift+Alt+F3 |
| Toggle sticky window in desktops | Shift+Alt+F4 |

> Note To be able to use your keyboard properly during your X11 sessions, make sure you've configured X with the correct keyboard setting for your computer. See Chapter 4 for details about the XFConfig file.

## Features of the icew Window Manager

The icew window manager (in Figure 5.5) is designed to look like OS/2 or Windows 95 (and other window managers). It features numerous mouse and keyboard commands, and its configuration files and directories are located under /usr/X11R/lib/X11/icew manager. To start an X session window manager, type start icew at the command line and press Enter.

```
start icew
```

Figure 5.5 The icew desktop features an easy-to-use, if not minimalistic, X11 environment.

![](img/cbac72550c7126a22162e94d91a0c360_147_0.png)

## Features of the K Desktop Environment

KDE supports many of the features you'd expect in a modern desktop environment, including those commonly found in commercial software libraries, such as Motif, and the Common Desktop Environment or CDE (which is now only offered by one vendor, Xi-Graphics, for Linux). These features include:

- A suite of personal productivity tools, such as disk and network utilities, designed to use the desktop interface and the capability to import and export data to other tools
- Session management, so open applications and window positions are remembered between sessions
- "Sticky Buttons” to put an application or window on every desktop
- Network Transparent Access, or NTA, so you can click or drag and drop a graphic document’s icon in an FTP window to display or transfer the graphic
- Pop-up menus and built-in help for nearly any desktop action and KDE client
- A desktop trash can for safer file deletions
- Graphic configuration of your system’s desktop, keyboard, mouse, and sound
- Programs and other data represented as icons on the desktop or in windows with folder icons
- Drag-and-drop actions (such as copy, link, move, and delete) for files

## Introduction and Installation SuSE Linux

The fwm window manager (shown in Figure 5.3) is a descendant of the twm window manager but has several advantages, such as using less memory, supporting fancier window decorations, and providing virtual desktops.

**Figure 5.3**
The fwm window manager is an improvement over
The XII's twm window manager.

![](img/cbac72550c7126a22162e94d91a0c360_144_0.png)

You'll find fwm default file under the /usr/X11/lib/X11/fwm directory which is named system.fwmrc. Copy this file to your home directory as .fwmrc and make changes to customize it for your use. fwm startup file contains sections for customizing window colors and style, menus, and the number of virtual desktops. Look for the desktop section, which looks like the following:

```
# Set up the virtual desktop and pager
#set the desktop top size in units of physical screen size
DesktopSize 3x2
```

fwm's startup file defines different virtual desktops. You can move to a different desktop by pressing your left button on the appropriate square in the desktop pager's window. By changing the DesktopSize value you can either reduce or increase the number of virtual desktops. For example, a setting like the following to add another desktops:

DesktopSize 4x2

When you restart fwm, you'll see that two additional desktops have been added to the fwm pager. If you do not use an X11 display manager to log into KDE Linux, you can use fwm for your X11 session using the word in your start line:

```
startx fwm
```

## The fvwm Window Manager

fvvwm window manager (see Figure 5.4) is a configurable taskbar, window frames, buttons, scrollbars, and capability for extensive customization.

**Figure 5.4**
fvwm window manager provides many sophisticated window controls.

![](img/cbac72550c7126a22162e94d91a0c360_145_0.png)

This window manager's default startup file is found under /usr/X11R/lib/fvwm directory as system.fvwmrc. Copy this file to your home directory as .fvwmrc and make changes to customize your X11 sessions. If you do not use an X11 display manager to log in, insert fvwm in your start command line:

```
startx fvwm
```

fvwm features virtual desktops, a desktop pager, and window decorations. You can also use this window manager (like fwm) without an X11 pointing device. Table 5.1 lists nearly two dozen keyboard commands you can use to manipulate or move over windows.

### Table 5.1 Common Fvwm Keyboard Commands

| Command | Keyboard Command |
| :--- | :--- |
| Close current window | Alt+F9 |
| Display list of windows | Alt+F2 |
| Iconify current window | Alt+F4 |
| Jump to next window | Alt+F1 |
| Move current window | Alt+F5 |
| Next desktop down | Shift+Alt+down |
| Next desktop to left | Shift+Alt+left |
| Next desktop to right | Shift+Alt+right |
| Next desktop up | Shift+Alt+up |
| Pointer down 100 pixels | Shift+Ctrl+down |
| Pointer down 5 pixels | Shift+down |
| Pointer left 100 pixels | Shift+Ctrl+left |
| Pointer left 5 pixels | Shift+left |
| Pointer right 100 pixels | Shift+Ctrl+right |
| Pointer right 5 pixels | Shift+right |
| Pointer up 100 pixels | Shift+Ctrl+up |
| Pointer up 5 pixels | Shift+up |
| Resize current window | Alt+F6 |
| Toggle Maximize/normal window size | Shift+Alt+F3 |
| Toggle sticky window in desktops | Shift+Alt+F4 |

> Note To be able to use your keyboard properly during your X11 sessions, make sure you've configured X with the correct keyboard setting for your computer. See Chapter 4 for details about the XFConfig file.

## Features of the icew Window Manager

The icew window manager (in Figure 5.5) is designed to look like OS/2 or Windows 95 (and other window managers). It features numerous mouse and keyboard commands, and its configuration files and directories are located under /usr/X11R/lib/X11/icew manager. To start an X session window manager, type start icew at the command line and press Enter.

```
start icew
```

Figure 5.5 The icew desktop features an easy-to-use, if not minimalistic, X11 environment.

![](img/cbac72550c7126a22162e94d91a0c360_147_0.png)

## Features of the K Desktop Environment

KDE supports many of the features you'd expect in a modern desktop environment, including those commonly found in commercial software libraries, such as Motif, and the Common Desktop Environment or CDE (which is now only offered by one vendor, Xi-Graphics, for Linux). These features include:

- A suite of personal productivity tools, such as disk and network utilities, designed to use the desktop interface and the capability to import and export data to other tools
- Session management, so open applications and window positions are remembered between sessions
- "Sticky Buttons” to put an application or window on every desktop
- Network Transparent Access, or NTA, so you can click or drag and drop a graphic document’s icon in an FTP window to display or transfer the graphic
- Pop-up menus and built-in help for nearly any desktop action and KDE client
- A desktop trash can for safer file deletions
- Graphic configuration of your system’s desktop, keyboard, mouse, and sound
- Programs and other data represented as icons on the desktop or in windows with folder icons
- Drag-and-drop actions (such as copy, link, move, and delete) for files

## Introduction and Installation SuSE Linux

The fwm window manager (shown in Figure 5.3) is a descendant of the twm window manager but has several advantages, such as using less memory, supporting fancier window decorations, and providing virtual desktops.

**Figure 5.3**
The fwm window manager is an improvement over
The XII's twm window manager.

![](img/cbac72550c7126a22162e94d91a0c360_144_0.png)

You'll find fwm default file under the /usr/X11/lib/X11/fwm directory which is named system.fwmrc. Copy this file to your home directory as .fwmrc and make changes to customize it for your use. fwm startup file contains sections for customizing window colors and style, menus, and the number of virtual desktops. Look for the desktop section, which looks like the following:

```
# Set up the virtual desktop and pager
#set the desktop top size in units of physical screen size
DesktopSize 3x2
```

fwm's startup file defines different virtual desktops. You can move to a different desktop by pressing your left button on the appropriate square in the desktop pager's window. By changing the DesktopSize value you can either reduce or increase the number of virtual desktops. For example, a setting like the following to add another desktops:

DesktopSize 4x2

When you restart fwm, you'll see that two additional desktops have been added to the fwm pager. If you do not use an X11 display manager to log into KDE Linux, you can use fwm for your X11 session using the word in your start line:

```
startx fwm
```

## The fvwm Window Manager

fvvwm window manager (see Figure 5.4) is a configurable taskbar, window frames, buttons, scrollbars, and capability for extensive customization.

**Figure 5.4**
fvwm window manager provides many sophisticated window controls.

![](img/cbac72550c7126a22162e94d91a0c360_145_0.png)

This window manager's default startup file is found under /usr/X11R/lib/fvwm directory as system.fvwmrc. Copy this file to your home directory as .fvwmrc and make changes to customize your X11 sessions. If you do not use an X11 display manager to log in, insert fvwm in your start command line:

```
startx fvwm
```

fvwm features virtual desktops, a desktop pager, and window decorations. You can also use this window manager (like fwm) without an X11 pointing device. Table 5.1 lists nearly two dozen keyboard commands you can use to manipulate or move over windows.

### Table 5.1 Common Fvwm Keyboard Commands

| Command | Keyboard Command |
| :--- | :--- |
| Close current window | Alt+F9 |
| Display list of windows | Alt+F2 |
| Iconify current window | Alt+F4 |
| Jump to next window | Alt+F1 |
| Move current window | Alt+F5 |
| Next desktop down | Shift+Alt+down |
| Next desktop to left | Shift+Alt+left |
| Next desktop to right | Shift+Alt+right |
| Next desktop up | Shift+Alt+up |
| Pointer down 100 pixels | Shift+Ctrl+down |
| Pointer down 5 pixels | Shift+down |
| Pointer left 100 pixels | Shift+Ctrl+left |
| Pointer left 5 pixels | Shift+left |
| Pointer right 100 pixels | Shift+Ctrl+right |
| Pointer right 5 pixels | Shift+right |
| Pointer up 100 pixels | Shift+Ctrl+up |
| Pointer up 5 pixels | Shift+up |
| Resize current window | Alt+F6 |
| Toggle Maximize/normal window size | Shift+Alt+F3 |
| Toggle sticky window in desktops | Shift+Alt+F4 |

> Note To be able to use your keyboard properly during your X11 sessions, make sure you've configured X with the correct keyboard setting for your computer. See Chapter 4 for details about the XFConfig file.

## Features of the icew Window Manager

The icew window manager (in Figure 5.5) is designed to look like OS/2 or Windows 95 (and other window managers). It features numerous mouse and keyboard commands, and its configuration files and directories are located under /usr/X11R/lib/X11/icew manager. To start an X session window manager, type start icew at the command line and press Enter.

```
start icew
```

Figure 5.5 The icew desktop features an easy-to-use, if not minimalistic, X11 environment.

![](img/cbac72550c7126a22162e94d91a0c360_147_0.png)

## Features of the K Desktop Environment

KDE supports many of the features you'd expect in a modern desktop environment, including those commonly found in commercial software libraries, such as Motif, and the Common Desktop Environment or CDE (which is now only offered by one vendor, Xi-Graphics, for Linux). These features include:

- A suite of personal productivity tools, such as disk and network utilities, designed to use the desktop interface and the capability to import and export data to other tools
- Session management, so open applications and window positions are remembered between sessions
- "Sticky Buttons” to put an application or window on every desktop
- Network Transparent Access, or NTA, so you can click or drag and drop a graphic document’s icon in an FTP window to display or transfer the graphic
- Pop-up menus and built-in help for nearly any desktop action and KDE client
- A desktop trash can for safer file deletions
- Graphic configuration of your system’s desktop, keyboard, mouse, and sound
- Programs and other data represented as icons on the desktop or in windows with folder icons
- Drag-and-drop actions (such as copy, link, move, and delete) for files

## Introduction and Installation SuSE Linux

The fwm window manager (shown in Figure 5.3) is a descendant of the twm window manager but has several advantages, such as using less memory, supporting fancier window decorations, and providing virtual desktops.

**Figure 5.3**
The fwm window manager is an improvement over
The XII's twm window manager.

![](img/cbac72550c7126a22162e94d91a0c360_144_0.png)

You'll find fwm default file under the /usr/X11/lib/X11/fwm directory which is name system. .fwmrc. Copy this file to your home directory .fwmrc and make
changes to customize it for your use. fwm startup file contains sections for customizing
window colors and style, menus, and the number of virtual desktops. Look for the desktop
section, which looks like the following:

```
# Set up the virtual desktop and pager
#set the desktop top size in units of physical screen size
DesktopSize 3x2
```

fwm's startup file defines different virtual desktops. You can move to a different
desktop by pressing your left button on the appropriate square in the desktop pager's
window. By changing the DeskTop value you can either reduce or increase the number of virtual desktops. For example, a setting like the following to add another desktops:

DeskTop 4x2

When you restart fwm, you'll see that additional two desktops have been added to
fvwm pager. If you do not use an X11 display manager to log into SuSE Linux, you can use fwm for your X11 session using the word **fvwm** in your start line:

```
# startx fwm
```

# The fvw2 Window Manager

fvv2 window manager (see Figure 5.4) is a configurable taskbar, window frames, buttons, scrollbars, and capability for extensive customization.

**5.4**
Thevw2 window manager provides many sophisticated window controls.

![](img/cbac72550c7126a22162e94d91a0c360_145_0.png)

This window manager's default startup file is found under /usr/X11R/lib/fvwm directory as system.fvwmrc. Copy this file to your home directory as .fvwmrc and make
changes to customize your X sessions. If you do not use an X11 display manager to log insert **fvwm2** in your **start command**:

```
# startx fvwm
```

fvwm features virtual desktops, a desktop pager, and configurable window decorations. You can also use this window manager (like fwm) without an X11 pointing device. Table 5.1 lists nearly two dozen keyboard commands you can use to manipulate or move over

# Table 5.1 Common Fwm Keyboard Commands

| Command | Keyboard Command |
| :--- | :--- |
| Close current window | Alt+F9 |
| Display list of windows | Alt+F2 |
| Iconify current window | Alt+F4 |
| Jump to next window | Alt+F1 |
| Move current window | Alt+F5 |
| Next desktop down | Shift+Alt+down |
| Next desktop to left | Shift+Alt+left |
| Next desktop to right | Shift+Alt+right |
| Next desktop up | Shift+Alt+up |
| Pointer down 100 pixels | Shift+Ctrl+down |
| Pointer down 5 pixels | Shift+down |
| Pointer left 100 pixels | Shift+Ctrl+left |
| Pointer left 5 pixels | Shift+left |
| Pointer right 100 pixels | Shift+Ctrl+right |
| Pointer right 5 pixels | Shift+right |
| Pointer up 100 pixels | Shift+Ctrl+up |
| Pointer up 5 pixels | Shift+up |
| Resize current window | Alt+F6 |
| Toggle Maximize/normal window size | Shift+Alt+F3 |
| Toggle sticky window in desktops | Shift+Alt+F4 |

> Note
To be able to use your keyboard properly during your X11 sessions, make sure you've configured X with the correct keyboard setting for your computer. See Chapter 4 for details about the XF6Config.

# Features of the icew Window Manager

The icew window manager (in Figure 5.5) is designed to look like OS/2 or Windows 95 (and other window managers). It features numerous mouse and keyboard commands, and its configuration files and directories are located under /usr/X11R/lib/X11/icew manager. To start an X session window manager, type start icew at the command line, and press Enter.

```
# start icew
```

Figure 5.5 The icew desktop features an easy-to-use, if not minimalistic, X11 environment.

![](img/cbac72550c7126a22162e94d91a0c360_147_0.png)

# Features of the K Desktop Environment

KDE supports many of the features you'd expect in a modern desktop environment, including those commonly found in commercial software libraries, such as Motif, and the Common Desktop Environment or CDE (which is now only offered by one vendor, Xi-Graphics, for Linux). These features include

+   * A suite of personal productivity tools, such as disk and network utilities, designed to use the desktop interface and the capability to import and export data to other tools
+   * Session management, so open applications and window positions are remembered between sessions
+   * "Sticky Buttons” to put an application or window on every desktop
+   * Network Transparent Access, or NTA, so you can click or drag and drop a graphic document’s icon in an FTP window to display or transfer the graphic
+   * Pop-up menus and built-in help for nearly any desktop action and KDE client
+   * A desktop trash can for safer file deletions
+   * Graphic configuration of your system’s desktop, keyboard, mouse, and sound
+   * Programs and other data represented as icons on the desktop or in windows with folder icons
+   * Drag-and-drop actions (such as copy, link, move, and delete) for files
