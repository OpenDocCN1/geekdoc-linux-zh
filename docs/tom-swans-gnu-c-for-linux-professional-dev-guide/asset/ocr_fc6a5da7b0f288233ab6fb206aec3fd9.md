these tests can degrade the program's performance, you might choose not to make them if you are writing an action game, but you'd probably want to perform the standard checks in a mathematical subroutine library.

Another reason the compiler does not normally optimize code is time. Each level of optimization increases compilation time and expands the amount of memory required during compilation. Also, with no optimizations selected, the compiler produces code that the GNU debugger can synchronize with the program's source text so that you can view statements and data. Because optimizations rearrange compiled code, use processor registers, and perform other tricks, it is more difficult to debug optimized code.

Other optimizations speed performance but can greatly expand the size of the executable code file. Depending on your needs, you might opt to have smaller code files in return for a small degradation in performance. On the other hand, if you have plenty of disk space, you probably want your programs to run as fast as possible regardless of how much real estate they stake out. The following sections describe various options that you can use to select different levels and types of optimizations.

# OPTIMIZATION LEVELS

General optimization options begin with -O (that's the capital letter O) either alone or followed by one of the digits 0, 1, 2, or 3. For example, to compile welcome.cpp from the preceding chapter using the first level of optimizations, specify -O1 to the compiler with this command:

```
$ g++ -O1 welcome.cpp
```

Level one is the default, so that's the same as typing -O alone. The equivalent command is

```
$ g++ -O welcome.cpp
```

Specify -O2 or -O3 to select additional levels of optimizations, which might result in even faster running code, but which also makes the compiler work a lot harder. The option -O0 (a capital O and a zero) is the same as not specifying any optimizations. Because the compiler normally performs no optimizations, you rarely have to specify -O0, but it might come in handy in a Makefile script that selects among optimization levels.

You can also select specific optimizations such as -ffast-math. These options begin with -f and are followed by the option name. There must be no space after -f. For example, the following command tells the compiler to ignore the inline keyword:

```
$ g++ -fno-inline
```

Inline functions, which you meet in Chapter 10, "Creating and Calling Functions," can greatly speed up some kinds of programs. They are an excellent example of the kinds of optimizations that you can perform in the program's source code. However, inline functions can also greatly expand the program's executable code file. Using the preceding option might cause the program to run a little slower, but it might also reduce its code file size significantly.