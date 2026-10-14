# Debugging

After you have successfully compiled and linked your program, it can be started from the shell by giving its name as command (a.out or ownname when compiled with -o ownname). This does not mean, however, that

+   1. your programm runs successfully to its end,
+   2. it complies with your intentions.

If some run-time error occurs, you have to debug the program. You can do this either manually (by printing out certain intermediate results and test statements), or you use a so-called debugger. Such a tool allows, e.g.,

+   - to execute the statements stepwise
+   - to view the current content of the variables
+   - to stop the program at so-called breakpoints defined by yourself.

An open source and window-oriented debugger available under Linux is ddd (Data Display Debugger), which works for C++ und Fortran programs (at least those compiled with g++ and gfortran, respectively, and with option -g).

The debugger is simply called via

```
ddd program_name
```

where program_name is the name of the executable object (e.g., a.out).

The core of ddd (which actually provides the window interface ‘only’) is the debugger gdb, which can be alternatively used alone to debug the program (from the console). It is called via

```
gdb program_name
```

but needs some knowledge of the involved commands.

Remember: To debug a program, it has to be compiled with the option -g in order to include the required debug information.

# Example:

```
wegner@arber:> gfortran -g hello.f90 -o fhello
wegner@arber:> ddd fhello
GNU DDD 3.3.11 (x86_64-suse-linux-gnu),
by Dorothea Luetkehaus and Andreas Zeller.
...
(gdb)
```

# Exercise:

+   1. Compile the program p1.f90 and run it. Re-compile with the option -g!
+   2. Start ddd for the executable object. Become acquainted with the most important entries (Run, Step, Next, ...) in the control panel und buttons (Break, Print) in the menu bar.