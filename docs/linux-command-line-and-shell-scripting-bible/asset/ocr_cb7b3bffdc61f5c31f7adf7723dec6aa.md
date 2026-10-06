When you use the bold (1) or blink (5) control codes in your script to highlight important text, you must change the foreground and background colors back, as there are no unfold or unblink control codes. Unfortunately, the reset control code just sets the display back to the default, to whatever setting you were previously using.

# Doing Windows

Using text menus and colors is a step in the right direction, but there's still a lot missing in our interactive scripts, especially if we try to compare them to the graphical Windows world. For-tunately for us, there are some resourceful people out in the open source world that have helped us out.

The dialog package is a nifty little tool originally created by Savio Lam, and continually maintained by Thomas E. Dickey. This package recreates standard Windows boxes in a text environment using ANSI escape codes. You can easily incorporate these dialog boxes in your shells to interact with your script users. This section describes the dialog package and demonstrates how to use it in shell scripts.

# The dialog package

The dialog command uses line parameters to determine what type of Windows widget to produce. A widget is the dialog package term for a type of Windows element. The dialog package currently supports the types of widgets shown in Table 15-3.

As you see from Table 15-3, there are lots of different widgets to choose from. This can give your scripts a more professional look with very little effort.

To specify specific widget on the command line, you need to use the double dash format:

```
dialog --widget parameters
```

Where widget is the widget name as seen in Table 15-3, and the parameters define the size of the widget window and any text required for the widget.

Each dialog widget provides output in two forms:

+   - Using STDERR
- Using the exit code status

The exit code status of the dialog command determines the button selected by the user. If an OK or Yes button is selected, the dialog command returns a zero exit status. If a Cancel or No button is selected, the dialog command returns a one exit status. You can use the standard $ variable to determine which button was selected in the dialog widget.