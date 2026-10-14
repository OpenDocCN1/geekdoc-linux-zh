is replaced with an elongated declaration that indicates class `string` is itself a complex nested template. Chapter 22, “Mastering the Standard string Class,” covers C++ string objects, so I won’t go into the declaration here. But it is highly interesting that you can use the GNU debugger to find out exactly how C++ instantiates template and other classes in the compiled program.

# SETTING BREAKPOINTS IN TEMPLATE CLASSES

Another useful method for setting breakpoints in template classes is to use the name of an instantiated class function instead of a source code line number. Reload the gdb program into the debugger, if necessary, and enter the following command to set a breakpoint in the `GetRecord()` member function (again, the line number might be different for you):

```
```text
(gdb) b 'TDatabase<Record>::GetRecord()
Breakpoint 3 at 0x80496e4: file db.h, line 36.
(gdb)
```
```

Actually, you don’t have to type all that. Just type `b 'T` (including the apostrophe), press Tab, type `::Get`, press Tab again, and you’re finished. In general, you can use command-line completion this way to enter lengthy identifiers—after all, the debugger knows all the symbols in the program and can easily search for matches using partial input.

> **Note**  
> I wonder why other debuggers don’t have handy features such as command-line symbol completion. Probably because you have to pay for the products!

After setting the breakpoint in `GetRecord()`, run or continue the program until it halts:

```
```text
(gdb) cont
Continuing.
Breakpoint 3, TDatabase<Record>::GetRecord (this=0x804b680,
  recnum=0) at db.h:36
36 if (0 <= recnum && recnum < num)
```
```

This time, the parameters to `GetRecord()` seem to be correct. You can now proceed to step through the instantiated function and examine the program’s exception handling. Type `q` when you’re finished.

> **Tip**  
> When the program is paused in a member function, the command `ptype this` displays the type of object for which the function was called.