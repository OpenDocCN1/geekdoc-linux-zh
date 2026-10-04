# Chapter 2. The Mechanics of Using the Tcl and Tk Interpreters

You can set the environment variable at your command line.

Using Bourne shell, Korn shell, or bash, this command would resemble:
TCL_LIBRARY=/usr/local/lib/tcl18.0p; export TCL_LIBRARY
Using csh, tcsh, or zsh, the command would resemble:
setenv TCL_LIBRARY /usr/local/lib/tcl18.0

When tcl is run with no command line, it will display a % prompt to let you know the interpreter is ready to accept commands.
When wish starts up, it will open a new window for graphics and will prompt the user with a % prompt in the window where you invoked wish.

# 2.1.3 Starting tcsh or wish under Microsoft Windows

When you install Tcl under Windows 95 or Windows NT, it will create a Tcl menu entry under the Programs menu and, within that menu, entries for tclsh and wish. When you select the tclsh menu item, Tcl will create a window for you with the tclsh prompt (%). If you select the wish item, it will open two windows: one for graphics and one with the familiar % prompt.

You can also invoke tclsh from a DOS window by typing the complete path and command name. Note that you may need to use the 8.3 version of a directory name under Windows 95.

Windows NT

```
C:\Program Files\tcl\bin\tclsh80.exe
C:\Program Files\tcl\bin\wish80.exe
```

Windows 95

```
C:\Progra-1\tcl\bin\tclsh80.exe
C:\Progra-1\tcl\bin\wish80.exe
```

Once you have the % prompt, you can type commands directly to the shell.
The commands you enter will be interpreted immediately. If your command creates a graphic widget, it will be displayed in the graphics window.