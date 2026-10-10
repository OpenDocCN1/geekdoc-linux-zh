The computer cannot think, so you have to do the thinking for it.

Runtime errors are more commonly called *bugs*.

# 25.5 Program Execution

The file containing the executable code is given the name a.out by the linker (unless you specify another name). To execute the program, all you have to do is type

```
$ a.out<Return>
```

If you *want* to save the executable code, you can use the mv command to give this file an appropriate name.

# 25.6 Errors

The easiest thing about programming is making errors. Programming errors come in several varieties:

+   • Logic errors. The computer does what you tell it to do, not what you want it to do. If you specify the wrong way to solve the problem—if you multiply when you should have divided, for instance—your program may run and produce output, but the output will not be correct.

+   • Syntax errors. A syntax error results when you violate one of the rules of the programming language. Such errors are often called compilation errors because they will be detected by the compiler when you try to compile the program.

+   • Runtime errors. More insidious than syntax errors are those errors that escape detection by the compiler. These are called runtime errors because they usually are not discovered until you run the program a few times. (And perhaps not even then—many runtime errors are never tracked down.)

# 25.7 Debugging

A serious runtime error, such as dividing by zero or taking the square root of a negative number, may cause the program to crash. When this happens, the program quits running and the UNIX shell sends you an error message of some sort. Usually, these messages are not very informative: they tell you that the program crashed, but they don’t always tell you the reason.

When a program aborts because of a runtime error, the system produces a core dump, which is a file containing a “snapshot” of the main memory at the time the program failed. This is put into a file named core.

The core file contains machine code, so it is not something you would try to read directly yourself. However, most UNIX systems include special programs called debuggers that are designed to help you exterminate bugs in your programs. A debugger can use the information in the core file to determine what the bug was and