```
<Key>F1: set-session-argument(failsafe) finish-field()\n
Ctrl<Key>Return: set-session-argument(failsafe) finish-field()\n
<Key>Return: set-session-argument() finish-field()

xlogin*borderWidth: 3
xlogin*Greeting: CLIENTHOST
xlogin*namePrompt: login:\V40
xlogin*fail: Login incorrect
#ifdef COLOR
xlogin*greetColor: CadetBlue
xlogin*failColor: red
*Foreground: black
*Background: #fffff0
#else
xlogin*Foreground: black
xlogin*Background: white
#endif

Xconsole.text.geometry: 480x130
Xconsole.verbose: true
Xconsole*iconic: true
Xconsole*font: fixed

Chooser*geometry: 700x500+300+200
Chooser*allowShellResize: false
Chooser*viewport.forceBars: true
Chooser*label.font: *new century schoolbook-bold-r-normal-*240-*
Chooser*label.label: XDMCP Host Menu from CLIENTHOST
Chooser*list.font: -*-*-medium-r-normal-0--*230-*-*c-*-iso8859-1
Chooser*Command.font: *new century schoolbook-bold-r-normal-*180-*
```

Almost all of the entries are self-explanatory and allow you to change the color, font, text size, or other aesthetic features of the XDM login display.

> **Exam Tip**
> XDM uses an `Xresources` file to configure the display properties of the login screen.

# Using X

+   **Objective 2.10 X**
+   
+   *   Identify and terminate runaway X applications. Identify and kill X applications that won't die after user ends an X-session. Example: netscape, tkrat, etc.
+   *   Install & Customize a Window Manager Environment. Select and customize a system-wide default window manager and/or desktop environment, demonstrate an understanding of customization procedures for window manager menus, configure menus for the window manager, select and configure the desired x-terminal (xterm, nvt, aterm etc), verify and resolve library dependency issues for X applications, export an X-display to a client workstation. Commands: Files: `xinitrc`, `Xdefaults`, various `.rc` files.