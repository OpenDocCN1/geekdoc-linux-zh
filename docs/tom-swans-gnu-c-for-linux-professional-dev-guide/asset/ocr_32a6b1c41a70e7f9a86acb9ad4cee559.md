path, file Makefile.dbg compiles a copy of xwelcome.cpp as xdebug.cpp with debugging enabled. Compile and run the program with these commands:

```
$ make -f Makefile.dbg
$ ./xdebug
ConfigureNotify event received
Expose event received
ConfigureNotify event received
Keypress detected
```

> Tip
> Notice that ConfigureNotify and Expose events are received for the new window. This is always true for a newly created and mapped window. The X server sends the first event to indicate the current size and position of the window because the window manager might have altered those values before showing the client window for the first time. After this, the Expose event tells the client to display the window's contents.

Also remember the time-tested C and C++ technique for making "assertions" about function results. To use this method in X clients, include the assert.h header file with the following directive:

```
#include <assert.h>
```

Next, use the assert() macro to test any true or false condition. Typically, assert() is applied to the result of a function that returns a pointer to a structure. If that pointer is NULL, we want the program to halt with an error that identifies where the problem occurred. Here's how to use assert() to test the result of connecting to the X server:

```
Display *display;    // X server display structure
...
display = XOpenDisplay(NULL);
assert(display);
```

If XOpenDisplay() returns NULL, assert() halts the program and displays an error message such as

```
xdebug: xdebug.cpp:28: int main(): Assertion `display' failed.
Aborted (core dumped)
```

This also dumps memory and the stack to a core file, which you can remove. To disable all assertions, compile the program with the option -DNDEBUG (defining NDEBUG).

# DEBUGGING WITH THE GNU DEBUGGER

Although debugging X clients using the GNU debugger can be difficult, this is still a good way to investigate the cause of a bug. It is especially helpful for inspecting the values of complex X structures. One useful trick is to set a breakpoint inside the client's event loop, and then use debugger commands to inspect event structure members. Although this produces a virtual ream of data, you may find the technique helpful for pinpointing the cause of a bug caused by the misuse of event data.