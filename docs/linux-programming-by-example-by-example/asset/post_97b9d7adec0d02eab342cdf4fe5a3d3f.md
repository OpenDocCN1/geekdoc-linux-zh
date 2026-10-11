
![](img/be588b36b489136ce784030a08a1d3d4_482_0.png)

## Example

After setting $EF\_ALIGNMENT to 0, recompiling, and rerunning the program, Electric Fence catches the small overrun in the program.

```
$ export EF_ALIGNMENT=0
$ gcc -g badmem.c -o badmem -lfence
$ ./badmem
```

![](img/be588b36b489136ce784030a08a1d3d4_482_1.png)

## Output

```
Electric Fence 2.0.5 Copyright (C) 1987-1998 Bruce Perens
Segmentation Fault (core dumped)
$ gdb badmem
(gdb) run
Starting program: /usr/local/newprojects/lpe/20/src/badmem
Electric Fence 2.0.5 Copyright (C) 1987-1998 Bruce Perens.

Program received signal SIGSEGV, Segmentation fault.
strcpy (dest=0x4010affb "abcde", src=0x80495e8 "abcde")
    at ../sysdeps/generic/strcpy.c:38
../sysdeps/generic/strcpy.c:38: No such file or directory.
(gdb) where
#0 strcpy (dest=0x4010affb "abcde", src=0x80495e8 "abcde")
    at ../sysdeps/generic/strcpy.c:38
#1 0x80488c2 in main () at badmem.c:21
#2 0x40030cb3 in __libc_start_main (main=0x8048890 <main>, argc=1,
    argv=0xbffff934, init=0x8048860 <int>, fini=0x80495ac <_fini>,
    rtld_fini=0x4000a350 <dl_fini>, stack_end=0xbffff92c)
    at ../sysdeps/generic/libc-start.c:78
(gdb)
```

As you can see from the output, Electric Fence now catches the smaller overrun. I recommend always setting the EF\_ALIGNMENT environment variable to 0 and using the other variables discussed to catch as many memory bugs as possible.

> **TIP**
> During the development phase, a good practice might be always to link your programs against libfence to catch memory errors that might not otherwise get caught, precisely because of the memory alignment issues discussed previously.

## Using mpr and mcheck

The other memory debugging tool to consider using is Taj Khattria's mpr package, available from your favorite Metalab mirror (ftp://metalab.unc.edu/pub/Linux/devel/lang/c/mpr-1.9.tar.gz). It can be used to find memory leaks, but it does not find memory corruption errors. In addition, mpr also generates allocation statistics and patterns, but those features are not covered in this section. mpr's method uses simple brute force: It logs all allocation and free requests to an external log file that it later processes using utility programs that are part of the package.

### Using mpr

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

![](img/be588b36b489136ce784030a08a1d3d4_483_0.png)

### Example

This examples compiles badmem to use mpr to locate a memory leak.

```
$ gcc -g badmem.c -o badmem -Impr -L/usr/local/lib
$ export MPRPC='mprpc badmem'
$ export MPRFI="cat > badmem.log"
$ ./badmem
```

![](img/be588b36b489136ce784030a08a1d3d4_484_0.png)

### Output

```
LITTLE : abcde
mcheck: memory clobbered past end of allocated block
Aborted (core dumped)
$ mpr -f badmem < badmem.log | mprkl
m:main(badmem.c,18):10:13456992
```

The -f option reports the filename and line number where mpr detects the leak. The output indicates that line 18 of badmem.c in the main function mallocs 10 bytes of memory that it never frees (mpr and its utilities use the long decimal number to keep track of each allocation and free request). Referring to the code listing, you can see that this is correct.

### Using mcheck

As mentioned a moment ago, mpr, on its own, cannot detect memory-corruption errors. Although this is true, mpr includes the mcheck function from GNU's malloc library, which enables you to detect buffer overruns, buffer underruns, and multiple frees of the same block. In fact, mpr compiles mcheck into libmpr.a by default.

So, the good news is that the buffer overruns and underruns cause it to abort unless you specifically instruct mpr not to use mcheck. The bad news is that mcheck is not terribly informative—it merely complains about a problem and leaves the programmer to determine where the problem occurs. Compiled with mcheck, the sample program aborts each time you clobber memory.

![](img/be588b36b489136ce784030a08a1d3d4_484_1.png)

### Example

This example shows several runs of badmem compiled with mcheck, each run fixing the error encountered in the previous run:

![](img/be588b36b489136ce784030a08a1d3d4_484_2.png)

### Output

```
$ ./badmem
LITTLE : abcde
mcheck: memory clobbered past end of allocated block
* . . .
$ ./badmem
LITTLE : abcde
BIG : abcdefgh
UNDERRUN: abcdefgh
mcheck: memory clobbered before allocated block
[ . . . ]
$ ./badmem
LITTLE  : abcde

BIG     : abcdefgh
UNDERRUN:
mcheck: block freed twice
```

Fixing the rest of the errors is left as an exercise for you.

## What's Next?

You started building your debugging skills in this chapter. In the next chapter, "Software Distribution," you will learn a couple of methods for distributing your newly bug-free software. At the end of that chapter, you put all your skills together and build the programming project, a music CD database.

# 21—Software Distribution

The fastest, coolest code in the world will become shelfware if it is extraordinarily difficult to install or renders a user's system useless after installing it. Typically overlooked in programming texts, this chapter covers the tricky process of software distribution. You will learn the following:

-   Using the `tar` command
-   Using the `gzip` command
-   Using the `install` command
-   Using the Red Hat Package manager

*Software distribution* is the creation, distribution, installation, and upgrade of software in both source code and binary form. This chapter looks at the GNU project's `tar`, `gzip`, and `install` utilities and Red Hat's Red Hat Package Manager, RPM.

## Using tar and gzip

`tar` and `gzip` were for many years the standard UNIX utilities for creating and distributing source code. For many people, they still are. They have limitations, however, when it comes to maintaining system integrity, particularly because they don't have a built-in facility for managing version control or checking software dependencies. This should not be seen, however, as `tar` or `gzip`'s shortcoming. The assumption behind software distribution using `tar`, `gzip`, and `install` is that the user or system administrator will take care of versioning and dependencies.

## tar Usage

`tar`, which stands for *Tape ARChiver*, creates, manages, and extracts multfile archives, known as *tarfiles*, or, more affectionately and idiomatically, *tarballs*. `tar` is the traditional utility used to create archives. `tar` is blessed (or plagned, depending on your perspective) with a bewildering variety of command-line options and switches.

> **NOTE**
> Long-time UNIX users will notice the absence of the `cpio` command. Why? The Linux idiom is to use `tar` (and `gzip`) to create multiple file archives for distributing software. `cpio`, when it is used at all, is used to create and manage system backups. Indeed, in the seven years I have been using Linux, I have never encountered any software that was packaged using `cpio`. That is not to say it does not happen, of course. I just have not run across it.

This chapter attempts to manage the confusion by focusing on simple, typical usage as related to the creation and management of software distribution. Table 21.1 lists some of `tar`'s command-line options, which subsequent sections discuss in more detail.

Table 21.1: `tar` Command-Line Options

| Option | Description |
| :----- | :---------- |
| c | Creates an archive |
| f *archive_name* | A required argument, f *archive_name* tells tar the name of the tarball with which to work |
| r | Appends files to the archive |
| u | Updates existing files in the archive |
| t | Lists the contents of the archive |
| v | Generates verbose output |
| z | Creates or works with a compressed archive (`gzip` is the default compression utility) |
