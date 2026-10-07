# TABLE 27.2. BASIC GDB COMMANDS.

| Command | Description |
| :--- | :--- |
| file | Loads the executable file that is to be debugged. |
| kill | Terminates the program you are currently debugging. |
| list | Lists sections of the source code used to generate the executable file. |
| next | Advances one line of source code in the current function, without stepping into other functions. |
| step | Advances one line of source code in the current function, and does step into other functions. |
| run | Executes the program that is currently being debugged. |
| quit | Terminates gdb. |
| watch | Enables you to examine the value of a program variable whenever the value changes. |
| break | Sets a breakpoint in the code; this causes the execution of the program to be suspended whenever this point is reached. |
| make | This command enables you to remake the executable program without quitting gdb or using another window. |
| shell | Enables you to execute UNIX shell commands without leaving gdb. |

From the programmer's perspective, you have more details to be aware of when debugging C++ code than when you are debugging C code. This is because of the C++ features such as virtual functions and exception handling. gdb has added features to support debugging both of these C++ specific features.

# ## Debugging Virtual Functions

As described in the "Polymorphism" section of this chapter, virtual functions are C++'s way of implementing polymorphism. This means that there may be more than one function in a program with the same name. The only way to tell these functions apart is by their signatures. The signature of a function is composed of the types of all the arguments to the function. For example, a function with the following prototype has a signature of int, real:

```
void func(int, real);
```