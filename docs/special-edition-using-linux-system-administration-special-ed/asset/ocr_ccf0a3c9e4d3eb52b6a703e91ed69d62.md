# Customizing the xdm Login Prompt

The `/etc/X11/xdm/Xresources` or `/etc/X11R6/xdm/Xresources` file controls the appearance of the xdm login window. The file contains a series of X resource entries defining the appearance and behavior of xdm. The following is a typical Xresources file:

```
```text
! $XConsortium: Xresources /main/8 1996/11/11 09:24:46 swick $
xlogin*login.translations: #override\\
        Ctrl<Key>R: abort-display()\\n\\
        <Key>F1: set-session-argument(failsafe) finish-field()\\n\\
        <Key>Return: set-session-argument(failsafe) finish-field()\\n\\
        <Key>Return: set-session-argument() finish-field()\\n
xlogin*borderWidth: 3
xlogin*greeting: CLIENTHOST
xlogin*namePrompt: login:\040
xlogin*fail: Login incorrect
#ifdef COLOR
xlogin*greetColor: CadetBlue
xlogin*failColor: red
*Foreground: black
*Background: #ffffff
#else
xlogin*Foreground: black
xlogin*Background: white
#endif

XConsole.text.geometry: 480x130
XConsole.verbose:       true
XConsole*iconic:        true
XConsole*font:          fixed

Chooser*geometry:        700x500+300+200
Chooser*allowShellResize: false
Chooser*viewPort.foreBars: true
Chooser*label.font:      *-new century schoolbook-bold-i-normal--*-240-*
Chooser*label.label:     XDMCP Host Menu from CLIENTHOST
Chooser*list.font:       -*-*-medium-r-normal--*-230-*-c-*-iso8859-1
Chooser*Command.font:    *-new century schoolbook-bold-r-normal--*-180-*
```
```

X resource entries are grouped into classes where, typically, a single application or resource has its own class. For instance, in the Xresources file, the xlogin class controls the appearance and behavior of the xdm login window and the chooser class handles the appearance and behavior of the chooser.

Resource entries take the following standard form:

```
```text
<class name>*<resource name>: <value>
```
```

In the sample Xresources file above, several key entries control the appearance of the xdm login window:

+   - **xlogin*borderWidth:** Specifies the width of login window’s border in pixels.
+   - **xlogin*greeting:** Specifies the greeting title to display at the top of the xdm login window. The special keyword CLIENTHOST will be replaced with the hostname of the xdm system.