after these instructions have executed. (Its reasoning: Your program won't
work correctly until they've executed, so why waste the time stepping
through them?) So, when you request a breakpoint on the main program
with this command:

```
break main
```

gdb will actually set a breakpoint six instructions after the label main.
This guarantees that the stack frame has been set up, allowing you to
access variables on the stack. These variables include any command
line parameters passed to your program at startup, so it is an important
consideration.

If you really and truly do to set a breakpoint precisely at the main
label, you need to execute this command:

```
break *main
```

There's not a whole lot of advantage in it, unless you want to watch
stack frame setup actually happen. (There's nothing wrong with that, of)
course. But once you've seen it happen a time or two there's not much
sense in watching it every time you debug!

# Providing Command-Line Arguments

It's often useful to be able to provide command-line arguments when
debugging a program. Doing it is easy: Just follow the run command
with whatever you would type on the command line for the
program, exactly as you would type them:

```
(gdb) run fee foe foe
```

Here, four command-line arguments will be passed to the program
running under gdb. One nice touch is that these same arguments will
be retained by gdb and used every time you begin program execution
with the run command. That is, you don't have to retype them
time you run to start program execution again. (Obviously, they are
lost when you exit gdb.)

If you want to provide a different set of command-line arguments while
debugging the same program, you can use the set args command to
enter a new set:

```
(gdb) set args foo bar bas bat
```

And if you've forgotten precisely which arguments are being stored by
gdb for your next program run, you can display them with show args: