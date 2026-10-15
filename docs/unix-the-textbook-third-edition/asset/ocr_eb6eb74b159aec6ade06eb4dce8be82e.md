# 17.7.1.6 Setting Breakpoints

Viewing execution of all or part of your code statement by statement is called program/code tracing. In order to trace code, you need to set breakpoints in your program. You can trace a program up to a particular statement or function by using the break command, as described in Table 17.1. It allows you to run a program without interruption until the control reaches the line or function that you want to study more closely. The process of stopping a program in this way is known as setting breakpoints. As shown in the previous section, the main function starts at line 14 but its first executable statement is at line 18. We set the breakpoint at the first executable statement in main() and run the program. The program stops execution at line 18, the only breakpoint we have set, having statement temp = s_val;

```
(gdb) break main
Breakpoint 1 at 0x40083f: file bugged.c, line 18.
(gdb) run
Starting program: /usr/home/sarwar/unix3e/ch17/gdb/bugged

Breakpoint 1, main () at bugged.c:18
18          temp = s_val;
Current language:  auto; currently minimal
(gdb)
```

# 17.7.1.7 Single-Stepping through Your Program

Always set breakpoints in your program to be able to view execution of all or part of your code statement by statement. The process of tracing program execution statement by statement is known as single-stepping through your program. Single-stepping, combined with tracing of variables, allows you to study program execution closely. Single-stepping can be done with the step command, which executes the next program statement, stepping into a function if the statement is a function call. You can use the next command to single-step through your code, but it executes a function into its entirety. If you are tracing a variable, it shows you the value of the variable when a statement within the scope of the variable executes. Run the help scope command to get more information about the scoping rules.

After setting the breakpoint at main and running the program in the previous session, we then run each statement of the program one by one by using the next command. After the third next statement, the control reaches the call to the get_input (PROMPT, temp); function at line 21 in the main() function. We then use the step command to step into and execute each statement in the get_input() function. The first step command takes control to the first executable statement in the get_input() function, the for loop. The second step statement prompts you for keyboard input. As soon as you hit <Enter> after typing Hello World!, the system displays the error message Program received signal SIGSEGV, Segmentation fault, along with the problematic source code statement and line number (30 in this case) and the value of the str variable. The hexadecimal number at the beginning of the second line of the error