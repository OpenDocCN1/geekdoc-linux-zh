# Figure 5.1
GNU's graphical debugger, xgdb.

![](bbox=[0.25, 0.12, 0.65, 0.65])

Another way to start xgdb is to select it from the Start menu, or if you don't use the Fvwm Windowslike interface, from whatever program menu your window manager provides. Be prepared to hunt for the debugger's parent menu. On my system, this was Start/Programs/Utilities/Mail. Obviously, the debugger has nothing to do with Mail utilities, and it took me a while to find it. I think it's all-around easier just to run xgdb from the console. In fact, I prefer to run many X programs this way.

Tip
Start xgdb from a console prompt without specifying a filename. When the debugger's window appears, click the File button and select a compiled program for debugging.

The graphical debugger's commands are similar to the console commands but are in the form of clickable buttons. To run the program, click the Run button. To set a breakpoint, click the line in the top window's source code and then click the Break button. You see a red hand next to the line—at least, that's what my version of xgdb shows.

Click Run to execute up to a breakpoint, and observe the bottom window for any messages. The debugger's output is the same as explained in the preceding section. However, it's much handier to see the source code at the same time. Click Continue to continue the program after it halts at a breakpoint.