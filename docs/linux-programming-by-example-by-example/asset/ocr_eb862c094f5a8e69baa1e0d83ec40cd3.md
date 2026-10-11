# Using mpr and mcheck

The other memory debugging tool to consider using is Taj Khattria's mpr package, available from your favorite Metalab mirror (ftp://metalab.unc.edu/pub/Linux/devel/lang/c/mpr-1.9.tar.gz). It can be used to find memory leaks, but it does not find memory corruption errors. In addition, mpr also generates allocation statistics and patterns, but those features are not covered in this section. mpr's method uses simple brute force: It logs all allocation and free requests to an external log file that it later processes using utility programs that are part of the package.

# Using mpr

To use mpr, download and compile it. The package includes several utility programs and a static library, libmpr.a, against which you link your program. Be sure to use the -g switch to generate debugging symbols because some of mpr's programs require them.

Recall from Chapter 1, "Compiling Programs," that -lmpr links badmem against libmpr.a, and -L $ HOME//lib prepends $ HOME//lib to the library search path. After the program is compiled and linked, set the environment variables $ MPRPC to 'mprpc badmem' and $ MPRFI to "cat > badmem.log", mpr, uses $ MPRPC to traverse and display the call chain for each allocation and free request, while $ MPRFI defines a pipeline command for logging and, optionally, filtering mpr's output.

With these preliminary steps out of the way, execute the program. If all goes as planned, you should wind up with a file named badmem.log in the current directory. It will look something like the following:

```
m:134522506:134516229:134514813:10:134561792
m:134522506:134516229:134514826:5:134565888
f:134522614:134520869:134514880:134565888
m:134522506:134516229:134514890:5:134565888
f:134522614:134520869:134514975:134565888
f:134522614:134520869:134514987:134565888
```

This log information is not very informative as is (the documentation explains the format, if you are interested); it merely provides the raw material for mpr's utility programs, which parse, slice, and julienne the log to create meaningful information. To view leaks, use the mpr and mprlk as illustrated in the following example.

![](bbox=[0.04, 0.68, 0.1, 0.74])

# Example

This examples compiles badmem to use mpr to locate a memory leak.

```
$ gcc -g badmem.c -o badmem -Impr -L/usr/local/lib
$ export MPRPC='mprpc badmem'
```