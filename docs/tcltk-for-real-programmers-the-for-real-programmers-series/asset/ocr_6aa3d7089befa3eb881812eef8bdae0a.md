# Example 8.11-1

Example Script

```
# Create a label in the original window
#
label .1 -text "I'm in the original window"
# Create a new window, and a label for it
#
toplevel.otherTopLevel
label .otherTopLevel.1 -text "I'm in the other window"
# Display the labels.
#
pack .1
pack .otherTopLevel.1
```

Script Output

![](bbox=[0.303, 0.439, 0.513, 0.483])

![](bbox=[0.653, 0.439, 0.843, 0.483])

By default, the window name is shown in the top window decoration. This can be modified with the wm title command. The wm command gives the Tk programmer access to the services provided by the window manager. These services vary slightly between window managers and operating systems. You should read the online documentation for the subcommands supported by the wm command.

# 8.12 Interacting with the Event Loop

The Tk event loop is processed whenever the interpreter is not evaluating a command or procedure. It's best to write your code to spend as little time as possible within procedures. However, some tasks just take a while, and you may need to schedule passes through the event loop while your procedure is running.