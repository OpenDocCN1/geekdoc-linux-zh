# **TIP**

gdb is usually compiled with support for the GNU `readline` library, which means that it supports the command-line editing and history features of the bash shell. For example, to recall a previous command, use the up arrow key to scroll back through the command history.

+   · Ctrl+A moves to the beginning of the current line.
+   · Ctrl+D deletes the character under the cursor.
+   · Ctrl+E moves to the end of the current line.
+   · Ctrl+K deletes everything between the cursor's current location and the end of the line.

See the `readline` manual page for more details about command-line editing.

# Setting Breakpoints

As you debug problematic code, it is often useful to halt execution at some point, gdb enables you to set breakpoints on several different kinds of code constructs, including line numbers and function names. You can also set conditional breakpoints, where the code stops only when a certain condition is met.

To set a breakpoint on a line number, use the following syntax:

```
(gdb) break linenum
```

To set a breakpoint on a function name, use

```
(gdb) break funcname
```

gdb will halt execution before executing the specified line number or entering the specified function. You can then use `print` to display variable values, for example, or use `list` to review the code that is about to be executed. If you have a multi-file project and want to halt execution on a line of code or in a function that is not in the current source file, use one of the following forms:

```
(gdb) break filename:linenum
(gdb) break filename:funcname
```

Conditional breakpoints are usually more useful. They allow you to halt program execution temporarily when a particular condition is met. The correct syntax for setting conditional breakpoints is as follows:

```
(gdb) break linenum or funcname if expr
```

expr can be any expression that evaluates to `TRUE` (nonzero). To resume executing after hitting a breakpoint, type `continue`. If you have set many breakpoints and have lost track of what has been set and which ones have been triggered, you can use the `info breakpoints` command to refresh your memory. The `delete` command allows you to delete breakpoints, or you can