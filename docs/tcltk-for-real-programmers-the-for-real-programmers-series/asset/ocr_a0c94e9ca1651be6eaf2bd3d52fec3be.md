# 2.2 Using tcl/wish Interactively

+   - The ability to save your commands in a file. This lets you experiment
with commands and save your work.
- A menu to load and run Tcl scripts from files.
- Support for opening new TkConsole displays.

This program is included in the CD-ROM accompanying this book. After
you install it, you can invoke it as any other script. Under MS-
Windows, start it via the RUN button, or move it into the Start menu.
Under Unix, type tkconsole_1.tcl at a shell prompt.

Note that although TkCon is easier to work with the interactive wish
interpreter, to invoke wish scripts, and is more powerful than
the Windows command interpreter, it does not deal well with programs that
require user interaction after they have been started. It's actually designed to
help Tcl scripts and to run noncommutative commands.

# 2.2.3 Evaluating Scripts Interactively

Tcl and wish can be used interactively as Tcl program interpreters. This
section will discuss typing a short program at the command prompt. The
next section will discuss how to run a program saved in a file.

The traditional first program, "Hello, world," is trivial in Tcl:

```
% puts "Hello, world"
Hello, world
```

The puts command sends a string to an I/O channel. By default, the stan-
dard output is your command window, but the output can be assigned to a
file, a TCP/IP socket, or through a pipe to another program. The details of
t Tcl commands will be covered in the next chapters.

Printing "Hello, world" is a fairly boring little, so let's make it a bit
more exciting by using the Tk extensions to make it into a graphics program.

In this case, you need to invoke the wish interpreter instead of the tsh
interpreter.

If you are using the TkConsole program to run these examples, you'll need
to load the Tk package by selecting the Interp menu, packages, and load Tk.