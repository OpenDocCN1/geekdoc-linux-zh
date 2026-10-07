Even though this is a very simple example. it illustrates the basic command syntax of the Tcl language. There are obviously many more commands contained within Tcl, but the basic syntax of all Tcl commands is the same:

command parameter1 parameter2 ...

The command can be any of the built-in Tcl commands. or it can be a user-defined extension to the Tcl command set in the form of a Tcl procedure. In either case, the fundamental syntax remains unchanged.

# What Is Tk?

Tk, which was also developed by Ousterhout, is a graphical user interface extension to Tcl. Tk is based on the X Window system and allows application developers to develop X Window-based applications much faster than they could using other X Window toolkits, such as Motif or Open Look. In many ways, you can think of Tk as similar to the Windows-based Visual language series (Visual Basic. for example).

Like Tcl, Tk also has a shell that enables you to enter commands to be interpreted. The Tk shell is a superset of the Tcl command shell. This means that anything you can do in the Tcl command shell can also be done in the Tk command shell. The big difference between the two is that the Tk command shell is designed to enable you to build X Window front ends to your applications.

The Tk command shell is called *wish*, which stands for windowing shell. You must be running an X Window application when you invoke *wish*. This is because when *wish* is invoked, it brings up a window that displays the results of any of the graphical commands it interprets.

Now that we have seen what the Tk environment looks like. let's try enhancing the earlier “Hello there” example by displaying Hello there in a button in the *wish* window. To accomplish this, we must first ensure that *wish* has been started. This is easily done by typing the following command into an Xterm window:

```
wish
```

This command brings up the *wish* window and also executes the Tk interpreter in the Xterm window. We can now type Tcl or Tk commands directly in the Xterm window. The commands necessary to print Hello there in a button in the *wish* window are as follows:

```
button .b -text "Hello there." -command exit
pack .b
```