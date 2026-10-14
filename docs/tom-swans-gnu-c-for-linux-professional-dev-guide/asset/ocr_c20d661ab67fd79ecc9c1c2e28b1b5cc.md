Now the program correctly halts inside the TContainer constructor. The debugger shows the parameter values passed to the constructor: this (the address of the object being constructed), and the value of n, equal in this case to the requested container size.

Tip
Type ptype this to find out the type of object addressed by a this pointer.

# DEBUGGING VIRTUAL FUNCTION CALLS

To debug a virtual function call, set a breakpoint in the base class that calls, for example, a pure virtual function in an abstract class. To demonstrate, load the tcontain program into the debugger if necessary (or type delete to erase all breakpoints if the program is currently loaded). Then, list the module containing a virtual function call—in this case, container.cpp. Again, supply a starting line number the first time you type list:

```
(gdb) list container.cpp:1
...
56 for (int i = 0; i < count; i++)
57 objects[i]->Display(); // Calls virtual function!
```

Line 57 calls the pure virtual function Display(). The goal is to find out, using the debugger, which actual Display() the program calls at runtime. To do that, set a breakpoint on the statement that calls the function:

```
(gdb) b 57
Breakpoint 3 at 0x80490b8: file container.cpp, line 57.
```

When you run the program, it halts at the breakpoint location:

```
(gdb) run
Starting program: /src/c15/tcontain
...
Breakpoint 3, TContainer::ShowAllObjects (this=0x804abf0, msg=0x8049fd <"Before sorting">) at container.cpp:57
57 objects[i]->Display(); // Calls virtual function!
```

To trace the virtual function call and discover what object's Display() function is bound to the statement, type a step command:

```
(gdb) step
TMyObject::Display (this=0x804ad98) at tcontain.cpp:71
71 cout << sp << " ";
```

The resulting output shows that TMyObject::Display() is bound at runtime to the statement that calls the pure virtual function TObject::Display(). Notice that the only argument passed to Display() is the address of the object. At this point, you can type cont to continue the program to its end (type cont again if this hits any breakpoints), and then type q to quit the debugger.