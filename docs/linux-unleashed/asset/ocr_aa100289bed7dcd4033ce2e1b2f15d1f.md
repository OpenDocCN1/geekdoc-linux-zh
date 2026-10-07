# # Tying It All Together: Working with make and RCS

The **make** program supports interaction with RCS, enabling you to have a largely complete software development environment. However, the whole issue of using **make** with RCS is a sticky one if your software project involves several people sharing source code files. Clearly, it may be problematic if someone is compiling files that need to be stable in order to do your own software testing. This may be more of a communication and scheduling issue between team members than anything else. At any rate, using **make** with RCS can be very convenient for a single programmer, particularly in the Linux environment.

**make** can handle RCS files through the application of user-defined suffix rules that recognize the `.v` suffix. RCS interfaces well with **make** because its files use the `.v` suffix, which works well within a suffix rule. You can write a set of RCS-specific suffix rules to compile C code as follows:

```
```
C0 = co
.c,V.o:
	$({C0}) $<
	$({CC}) $({CFLAGS}) -c $*.c
	- rm -f $*.c
```
```

The C0 macro represents the RCS check-out command. The `$*.c` macro is necessary because **make** automatically strips off the `.c` suffix. The hyphen preceding the `rm` command instructs **make** to continue, even if the `rm` fails. For `main.c` stored in RCS, **make** generates these commands:

```
```
co main.c
cc -O -c main.c
rm -f main.c
```
```

# ## Summary

Linux offers two key utilities for managing software development: **make** and RCS. **make** is a program that generates commands for compilation, linking, and other related development activities. **make** can manage dependencies between source code and object files so that an entire project can be recompiled as much as is required for it to be up-to-date. RCS is a set of source code control programs that enables several developers to work on a software project simultaneously. It manages the use of a source code file by keeping a history of editing changes that have been applied to it.