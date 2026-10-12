The basic and easiest of all the debugging techniques is to start adding print statements to the application code. Upon execution of the application, we can analyze the outputs from the print statements through which the cause of the problem can be narrowed down. Also, we would be able to immediately see whether the application layer is causing the problem. If the application is causing the issue, by using the print statements we would be able to narrow down the area of the application that causes the problem and take appropriate action.

# 3.3.1 gdb

The GNU debugger (gdb) allows us to examine the internals of another program while the program executes or retrospectively to see what a program was doing at the moment that it crashed. The gdb also allows us to examine and control the execution of code and is very useful for evaluating the causes of crashes or general incorrect behavior. gdb provides a text-based user interface, and it can be used to debug programs written in several languages (C, C++, and others). gdb can be used to perform the following operations, which are helpful in the process of debugging a compiled program:

+   - Setting up break points
+   - Displaying program values and attributes
+   - Execution step through line by line
+   - Information about the stake frame

gdb is run from the shell with the command gdb with the program name as a parameter, or we can use the file command once inside gdb to load a program for debugging. Both of these assume that you execute the commands from the same directory as the program. Once the executables' symbols are loaded, there are three ways to view the process with the debugger:

+   - View the running process using the attach command.
+   - Start the program using the run command.
+   - Use the core file to view the state of the process when it crashed.

In Example 3-33 we executed a simple program that does an illegal memory reference and fails with a segmentation fault.

*Example 3-33 Program execution that fails with a segmentation fault*

```
nx02:~# ./segfault
struct1->i : 40
struct1->j : 50
Segmentation fault
```