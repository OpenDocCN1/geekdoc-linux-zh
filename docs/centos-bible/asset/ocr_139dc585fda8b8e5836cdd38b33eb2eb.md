# **Part II**

# Using CentOS

# FIGURE 5-4

Select a program to run from the list in the Run Application window.

![](bbox=[0.15, 0.185, 0.46, 0.415])

When you have found an application and figured out the options that you like, you can add it to a menu or a panel if your window manager supports those features. In that way, you can run a program exactly as you want, instead of the way it is given to you on a menu.

Here is a procedure to run X applications from a Terminal window:

+   1. Open a Terminal window from your desktop.

+   2. Type

```
$ echo $DISPLAY
```

The result should be something similar to the following:

```
:0.0
```

This indicates that the Terminal window will, by default, direct any X application you run from this window to display 0.0 on your local system. If you don't see a value when you type that command, type **export DISPLAY=**:0.0 to set the display value.

+   3. With the *xmmms* package installed, type the following command:

```
$ xmmms &
```

The *xmmms* program should appear on your desktop, ready to work with. If you do not have the xmmms command, use the command *yum install xmmms* to install the program. You should note the following:

+   - The *xmmms* command runs in the background of the Terminal window (&). This means that you can continue to use the Terminal window while *xmmms* is running.

+   - I encountered no errors running *xmmms* on this occasion. With other applications, however, text sometimes appeared in the Terminal window after the command was run.