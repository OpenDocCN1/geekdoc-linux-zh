
previously used a computer with a mouse. A few, however, are likely to be new even to users familiar with the Macintosh and MS-Windows environments. The significant things to remember are:

- **X is designed for a three-button mouse**—Most X software makes use of the left button for pointing, clicking, and selection. X uses the center button for general functions such as moving or resizing windows, and the right button for application-specific functions such as opening in-application pop-up menus. Of course, any application is capable of modifying these uses, so examination of the documentation is always appropriate.
- **X has the concept of focused input**—On the Macintosh or MS-Windows platforms, if you type on the keyboard you generally expect the typing to appear in whatever window or dialog box is active—this isn’t the case with X Windows. In X, the window manager has the option of focusing your input anywhere it chooses. Most window managers can be configured to either focus input on the foremost window, focus input on a selected window (X does not have to be the foremost window), or focus input on whichever window the cursor is over. The last option, although unlike the interface you might be familiar with, is usually considered to be the most powerful. With the window manager configured so that focus follows the cursor, you can direct typing into a mostly hidden window—for example, to start a non-interactive program—by simply moving the cursor over any visible part of the mostly-hidden window and typing. No need to waste time bringing that window to the front, typing the command, and then shuffling the window back underneath the window that you really wanted to be working in.

![](img/2c005cbaad58c25c7f54da948131a75e_40_0.png)

> **If Your Input Disappears** If you're typing and you notice that what you're typing isn't appearing where you think it is supposed to be, chances are you've got your input focused in some other window. Check to make certain that your cursor is where it belongs, or—if your system is configured for click to focus—that you've clicked where you intend to type. It's very easy to get confused when moving between platforms using different input-focus methods.

In X, the window manager or any other program can attach arbitrary commands to arbitrary user actions. For example, a program can attach the action of displaying a menu when a user right-clicks on the title bar. The window manager can pop up a variety of menus when the user left-, right-, or center-clicks in the empty background of the windowing system; or it could happen when the user shift-left-, shift-right-, or shift-center-clicks— the possibilities are endless. One popular terminal program, xterm, pops up its configuration menus when the user holds down the control key and left-, right-, or center-clicks in the window. Some window managers attach a standard menu with common commands such as close and resize to each application's title bar. Others attach these functions to pop-up menus or buttons in the title bar. You'll find variations in program behavior even among different installations of the same UNIX flavor. Local configuration options can exert a significant influence over the interface. The best advice on how to find any particular option or command is to read the available documentation and to ask other local users.

Most window managers can iconize windows. Because the actual display of the client program's windows isn't handled by the client, the X server and window manager are free to make some useful contributions to the user experience. One of these contributions is that when the client requests a window with particular characteristics, the server isn't obliged to represent the window that way to the user—it is required only to treat it as though it had those characteristics. This enables the server to, for example, scale the window arbitrarily, or to shrink it down and treat it as an icon. If you're familiar with the idea of a task bar or application dock, you can think of iconized windows as windows that have been minimized, but that you can store anywhere on your screen.

## CONFIGURING X WINDOWS

Most configuration of X Windows is handled by a server resource database. When a client makes a request of the server, the server checks this database to determine user preferences for that client. The server resource database is loaded on a per-user basis via the command xrb, which needs to be executed automatically after starting X11. xrb loads configuration information from a dot file usually named .X11defaults. (Dot files are discussed in Lesson 16, "Modifying the User Environment".) .X11defaults usually contains lines similar to the following:

```
xbiff*onceOnly:		 on
xbiff*_wm_option.autoRaise:	 off
xbiff*mailBox:		 /usr/spool/mail/mymail
```

If you include these lines in your .X11defaults file, you are telling your X server that if xbiff (an X11 program that notifies you when you have new mail) starts, it needs to set certain options:

- Line 1 — Sets an xbiff-specific option regarding the frequency of ringing the bell to notify you.
- Line 2 — Sets an option regarding the window manager's treatment of xbiff—it specifically tells the window manager not to bring xbiff to the front if it's behind other windows when it needs to notify you. (Remember, X11 provides the display and a separate program provides management of things such as window controls.)
- Line 3 — Tells xbiff where to find the mailbox that it's supposed to look at.

Because each client supports different options and allows the window manager different levels of control, you'll need to consult each client's documentation to learn what you can configure and what you need to do to configure it.

In addition to the server resources database, clients frequently have command-line options that can control the client's interaction with X11. Take a look at the following command:

```
> xterm -fg "black" -bg "white" -fn 6x10 -geometry 85x30+525+1
```

This starts an xterm session with the following configuration: black as the foreground color, white as the background color (black text on a white window), and a 6x10 point font. It also sets the geometry information such that the window is 85 characters wide, 30 characters high, and placed 525 pixels from the left edge of the screen and 1 pixel down from the top.

Again, different programs have different options available and your local documentation is your best source for up-to-date information on your exact configuration.

## WINDOW MANAGERS

Because X Windows provides only rudimentary user-interface-component display functionality, an additional program is required to provide a useful user interface. This program is the window manager. Depending on the variation of UNIX you are running, you might have a number of options for different window managers. Each provides slightly different features with accordingly different strengths and weaknesses.

### twm

One of the most common—and least-featured—window managers is twm. twm, shown managing the display in Figure 3.1, provides very basic window management functions and is present or available on almost all UNIX implementations. If you work in a multi-platform environment with different flavors of UNIX, you might find twm to be convenient because your configuration can be identical on all the machines. For its simplicity, twm also provides some of the best user extensibility of the interface. If you like, you can create your own standard buttons that appear in your twm title bars to execute arbitrary commands. You can also build your own pop-up menus, automatically execute commands when the cursor enters windows, customize window manager colors and actions by application name and type, and a host of other customizations. To start the twm window manager, execute twm after starting X (you can probably do this automatically in your .xinitrc file). The control file for all this customization is named .twmrc and is probably located in your home directory.

As you can see in Figure 3.1, twm enables you to have a number of windows open at once. During window layering—even though windows might be partially covered by one another—you can focus input to the hidden windows, enabling you to work in any open window. Active applications that have been iconized can be clicked to be returned to their normal size.
