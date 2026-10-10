# ### Cross-Development Tools: the GNU Tool Chain

Not only is the target computer limited in resources, it may be a totally different processor architecture from your (probably) x86-based development workstation. Thus, we need a cross-development tool chain that runs on the PC but may have to generate code for a different processor. We also need a tool that will help us debug code running on that (possibly different) target.

# #### Gnu Compiler Collection

By far the most widely used compiler in the Linux world is GCC, the Gnu Compiler Collection. It was originally called the Gnu C Compiler, but the name was changed to reflect its support for more than just the C language. GCC has language front ends for C, C++, Objective C, Fortran, Java, and Ada, as well as run-time libraries for these languages.

GCC also supports a wide range of target architectures in addition to the x86. Supported targets include:

+   - Alpha
+   - ARM
+   - M68000
+   - MIPS
+   - PowerPC
+   - SPARC
+   among others. In fact, the Wikipedia article on GCC lists 43 processors and processor families supported by the Free Software Foundation version of GCC.

GCC can run in a number of operating environments, including Linux and other variants of Unix. There are even versions that run under DOS and Windows.

GCC can be built to run on one architecture (a PC for example), while generating code for a different architecture (an ARM perhaps). This is the essence of cross-development.

GCC is an amalgam of compiler, assembler, and linker. Individual language front ends translate source code into an intermediate assembly language format that is then assembled by a processor-specific assembler, and ultimately linked into an executable. For a program consisting of a single C source file, the command to build an executable can be as simple as:

```
```
   gcc myprogram.c
```
```

By default this creates an executable called `a.out`. The `-o` option lets you do the obvious thing and rename the executable thus:

```
```
   gcc -o myprogram myprogram.c
```
```