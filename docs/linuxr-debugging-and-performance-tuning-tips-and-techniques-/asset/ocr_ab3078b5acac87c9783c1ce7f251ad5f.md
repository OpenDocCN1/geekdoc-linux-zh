```
37 index = lsearch(NULL, NELEMS, 10); /* won't return */
38 
39 printf("index = %d\n", index);
40 
41 return 0;
42 }
```

When compiled and run, the assertion on line 12 “fires:”

```
$ ch12-assert Run the program
ch12-assert: ch12-assert.c:12: lsearch: Assertion ‘array != (\*void \*)0)’ failed.
Aborted (core dumped)
```

The message from assert() varies from system to system. For GLIBC on GNU/Linux, the message includes the program name, the source code filename and line number, the function name, and then the text of the failed assertion. (In this case, the symbolic constant NULL shows up as its macro expansion, `(\*void \*)0’).`

The “Aborted (core dumped)” message means that ch12-assert created a core file; that is, a snapshot of the process’s address space right before it died.² This file can be used later, with a debugger; see Section 15.3, “GDB Basics,” page 570. Core file creation is a purposeful side effect of assert(); the assumption is that something went drastically wrong, and you’ll want to examine the process with a debugger to determine what.

You can disable assertions by compiling your program with the command-line option `-DNDEBUG'. When this macro is defined before <assert.h> is included, the assert() macro expands into code that does nothing. For example:

```
$ gcc -DNDEBUG ch12-assert.c -o ch12-assert Compile with -DNDEBUG
$ ch12-assert Run it
Segmentation fault (core dumped) What happened?
```

Here, we got a real core dump! We know that assertions were disabled; there’s no “failed assertion” message. So what happened? Consider line 15 of lsearch(), when called from line 37 of main(). In this case, the array variable is NULL. Accessing memory through a NULL pointer is an error. (Technically, the various standards leave as “undefined” what happens when you dereference a NULL pointer. Most modern systems do what GNU/Linux does; they kill the process by sending it a SIGSEGV signal; this in turn produces a core dump. This process is described in Chapter 10, “Signals,” page 347.)

> ² As mentioned in Section 10.2, “Signal Actions,” page 348, some GNU/Linux distributions disable creation of core files. To reenable them, put the line ‘ulimit -S -c unlimited’ into your ~/.profile file.