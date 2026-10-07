are on the CD-ROM (including the one at the end of this book). The procedure FlagShip goes through to run an application is straightforward:

+   Preprocess the code to make sure there are no syntax errors or other common errors. If there are errors, issue error messages and terminate the compilation.
Convert to C code.
Compile with the system's C compiler to produce an object file.
Link the object file with FlagShip's libraries and produce an executable.

The executable thus produced can be run at the Linux command line prompt.

A quick word for dBASE and Clipper veterans: you needn't bother with overlays because UNIX has no need for them. Linux uses the virtual memory on your system to enable you to load any size application (although there are limits, they can be changed). Therefore, don't bother with overlays as you would with Clipper or other xBase compilers, and instead link your code into a single, large executable. Let Linux worry about loading it.

# ## dbMan

The dbMan program is an interpreter. When you start dbMan, you get a `CMD:` prompt. This is where you enter all your commands to dbMan. You can think of this as a `.` prompt in dBASE. For starters, you can type in `ASSIST`, at the `CMD:` prompt. `ASSIST` starts up a menu-driven interface similar to the ones available with FoxPro or dBASE.

The menu-driven interface is not very elaborate. `ASSIST` only enables one file to be open at a time, which means that it is not possible to set up relations. It is possible to start up a simple program generator from `ASSIST`. Again, it has a single file limitation.

You can compile programs in dbMan. Compiling a program does not produce an executable binary. It produces a `.run` file, which still requires dbMan to execute it. It is also possible to enter `CREATE REPORT` or `MODIFY REPORT` at the `CMD:` prompt. This puts you in dbMan's report writer. The report writer enables display of data by using the relational operators. dbMan provides a function called `PMENU()` to create pull-down menus. `PMENU` doesn't have any mechanism for temporarily disabling a menu choice.

dbMan handles windows differently from other xBase products. Prior to defining a window, you call `PUSHWND()` to push the current window onto a stack. When a program is in its initial state, the entire screen is considered to be a window. You then call `WINDOW()` to create the window. When you are finished with it, you call `POPWIND()`, which removes the window and makes the previous window active.

![](bbox=[0.87, 0.29, 0.97, 0.43])