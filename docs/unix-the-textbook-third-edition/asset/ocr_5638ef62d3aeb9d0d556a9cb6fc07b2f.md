```
lint $(LINTFLAGS) $(SOURCES)
...
% make lint
lint -c compute.c input.c main.c
...
%
```

Although lint checks for most portability features, it does not check a few things. It does not check whether control strings in the printf calls match the types of the corresponding variables. Nor does it ensure that variables are unique after the first seven characters. Other than these minor exceptions, lint is trouble free and should be used regularly to remove sticky stuff from production software.

# 17.6.2 Source Code Metrics

You can use the UNIX tool prof to display a profile of your code in terms of the functions used and the percentage of time taken by each function. This information allows you to focus more closely on those functions that are causing bottlenecks in the software.

At times, you will want to know how long a program spends in each function when it is executed. You can use this information to improve the performance of certain portions of a program by optimizing them. UNIX has two main tools for analyzing the program performance: prof and gprof. Both tools enable your program to track down the number of times each function is called and the time spent in each function. The gprof tool provides more data than prof, but both are effective in identifying expensive portions of your program and execution paths in it. The use of both tools is very similar, and they generate similar output. We discuss prof only, but the steps shown work for gprof as well.

The first step in using prof is to compile your program with a particular option that asks the compiler to insert appropriate code in the object module for counting the number of times that each function is executed and the time spent in each function. For fully testing your program, use the cc compiler command with the -p option, as in:

```
% cc -p matrix_mult.c -o mm
%
```

After your program has compiled successfully, run it. Execution produces the run-time data in a file called mon.out in a format that prof can read. You then use the prof utility with this file to display the program profile. The gprof tool is available on both PC-BSD and Solaris. However, prof is available on Solaris only.

# 17.7 DYNAMIC ANALYSIS TOOLS

Dynamic analysis of a program involves its analysis during run time. As we mentioned before, this phase comprises debugging, tracing, and performance monitoring of the software, including testing it against product requirements. In this section, we discuss the two useful UNIX tools for tracing the execution of a program and debugging (gdb), and measuring the running time of a program in actual time units (time).