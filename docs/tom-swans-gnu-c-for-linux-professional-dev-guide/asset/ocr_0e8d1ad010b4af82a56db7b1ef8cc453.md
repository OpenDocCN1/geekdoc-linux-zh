You might want to browse through some of gdb’s help pages—if you do, you’ll discover that the GNU debugger offers a full suite of commands for inspecting programs in just about any way imaginable. Now let’s get back to running welcome, which is paused inside the debugger, waiting for a command. To run the loaded program, type run:

```
(gdb) run
Starting program: /src/c05/welcome
Welcome to GNU C++ for Linux programming!
Program exited normally.
Current language: auto; currently c
(gdb)
```

When you give the run command, the debugger reads the program’s code and debugging information into memory. This takes a few moments. Eventually, the program runs and, in this case, displays the welcome string shown here on the third line. The debugger tells you the program exited normally and that the language recognized is auto; currently c. (This is correct for C++.) The program remains loaded into the debugger. To run it again, type another run command.

Some debugger commands require a source file line number. To find line numbers, use the list command. For example, type

```
(gdb) list
13 int main()
14 {
15   cout << "Welcome to GNU C++ for Linux programming!" << endl;
```

To save space, I show only three lines. Onscreen, you see more. Type a second list command to view more lines. Type list n, where n is a line number, to center that line in the output. Armed with the program’s line numbers, you can use commands such as break, which sets a breakpoint. With a breakpoint set, the debugger halts the program just before reaching the specified breakpoint location. You may set as many breakpoints as you need.

To try out breakpoints, find the line number of the statement where you want to pause execution. To set a breakpoint at line 15, enter the following command:

```
(gdb) break 15
Breakpoint 1 at 0x804866b: file welcome.cpp, line 15.
```

The debugger tells you the number of the breakpoint (1) and its address in memory. It also identifies the source code filename and the line number associated with this breakpoint. Run the program by giving the run command:

```
(gdb) run
Starting program: /home/tswan/mgcc/c05/welcome
Breakpoint 1, main () at welcome.cpp:15
15 cout << "Welcome to GNU C++ for Linux programming!" << endl;
```

When execution reaches the breakpoint, the program pauses. The debugger tells you that Breakpoint 1 stopped the program, and you see onscreen the line of code at that location.

To execute only that statement, issue a next command:

```
(gdb) next
Welcome to GNU C++ for Linux programming!
16 return 0;
```