
### Table 27-6: (continued)

| Parameter | Description |
|---|---|
| -q | Display the call graph analysis |
| -Q | Do not display the call graph analysis |
| -y | Generate annotated source code as separate output files |
| -Z | Do not display total tally of functions and number of times called |
| --function-reordering | Display suggested reordering of functions based on analysis |
| --file-ordering | Display suggested object file reordering based on analysis |
| -T | Display output in traditional BSD style |
| -w | Set width of output lines |
| -x | Display every line in annotated source code within a function |
| --demangle | Demangle C++ symbols when displaying output |

The analysis parameters modify the way gprof analyzes the data contained in the analysis file. These parameters are shown in Table 27-7.

### Table 27-7: The gprof Analysis Parameters

| Parameter | Description |
|---|---|
| -a | Do not analyze information about statistically declared (private) functions |
| -c | Analyze information on child functions that were never called in the program |
| -D | Ignore symbols that are not known to be functions (only on Solaris and HP OSs) |
| -k | Do not analyze functions matching a beginning and ending symspec |
| -l | Analyze the program by line instead of function |
| -m | Analyze only those functions called more than a specified number of times |
| -n | Analyze only the times for specified functions |
| -N | Do not analyze times for specified functions |
| -z | Analyze all functions, even those that were never called |

Finally, the miscellaneous parameters modify the behavior of gprof but don’t fit into the output or analysis groups. The miscellaneous parameters are described in Table 27-8.

### Table 27-8: The gprof Miscellaneous Parameters

| Parameter | Description |
|---|---|
| -d | Put gprof in debug mode, specifying a numerical debug level |
| -o | Specify the format of the profile data file |
| -s | Force gprof to summarize only the data in the profile data file |
| -v | Print the version of gprof |

To be able to use gprof on an application, you must ensure that the functions you want to monitor are compiled using the -pg parameter in the gcc program. This parameter compiles the source code, inserting a call to the mcount subroutine for each function in the program. When the application is run, the mcount subroutine creates a call graph profile file, called gmon.out, which contains timing information for each function in the application.

> Be careful when running the application, because each run will overwrite the gmon.out file. If you want to take multiple samples, you must temporarily rename the gmon.out files but then change them back when you are ready to run gprof.

After the test program finishes, the gprof program is used to examine the call graph profile file to analyze the time spent in each function. The gprof output contains three reports:

-   A flat profile report, which lists total execution times and call counts for all functions
-   A list of functions sorted by the time spent in each function and its children
-   A list of cycles, showing the members of the cycles and their call counts

By default the gprof output is directed to the standard output of the console. You must redirect it to a file if you want to save it.

### A Profile Example

To use the gprof program, you must have a high-level language program that uses functions to perform actions. I created a simple demonstration program in C, called demo.c, to demonstrate the basics of gprof:

```
#include <stdio.h>

void function1()
{
int i, j;
for(i=0; i <10000; i++)
j += i;
}
void function2()
{
    int i, j;
    function1();
    for(i=0; i < 200000; i++)
        j -= i;
}

int main()
{
    int i, j;
    for (i = 0; i <100; i++)
        function1();

    for(i = 0; i<50000; i++)
        function2();
}
```

This is about as simple as it gets. The main program has two loops—one that calls function1() 100 times and one that calls function2() 50,000 times. Each of the functions performs only simple loops, although function2() also calls function1() every time it is called.

The next step is to compile the program using the -pg parameter for gprof. After that the program can be run:

```
$ gcc -o demo demo.c -pg
$ ./demo
$
```

When the program finishes, the gmon.out call graph profile file is created in the same directory. You can then run the gprof program against the demo program and save the output to a file:

```
$ ls -al gmon.out
-rw-r--r-- 1 rich rich 440 2008-11-11 12:39 gmon.out
$ gprof demo > gprof.txt
$
```

Notice that the name of the executable program was referenced in the command line, but the gmon.out file was not. The gprof program automatically uses the gmon.out file located in the same directory.

This example redirects the output from the gprof program to a file named gprof.txt. The resulting file contains the complete gprof report for the program. You can view that file in any text editor. Here's what the flat profile section looked like on my system:

```
% cumulative self       self        total       calls  self ms/call  total ms/call name
time seconds seconds calls  us/call    us/call
67.02 22.78 22.78 50000 455.60 679.35 function2
32.98 33.99 11.21 50100 233.75 233.75 function1
```

This report shows the total processor time and times called for each individual function that was called by main. As expected, function2 took the majority of the processing time.
