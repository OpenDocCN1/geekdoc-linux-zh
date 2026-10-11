
12. You have several items available that you can provide in a `start_html` statement. These items are outlined in Table 21.5. This example simply sets the title and the target with:

```
-title=>'Thank you for participating',
-target=>"_blank'),
```

> **NOTE:** The double arrow (=>) is actually a shortcut for creating a hash pair.

13. Now you have an open Web document with its HTML `<HEAD>` tag properly in place. You can fill in the body, which is the following for this example:

```
$thankyou->"Thank you for filling in this information. We will only
use it for internal purposes.",
$thankyou->p;
```

14. Your **print** statement is now closed. You simply need to close the Web document. Use the **end_html** method to do this, in the following format:

```
$thankyou->end_html;
```

15. Press the Esc key to return to Command mode, and then type "ZZ" to save and close the file.

### Table 21.5 *Components available in the CGI Perl module's `start_html` statement.*

| Component | Purpose |
| :--- | :--- |
| **author** | Describes who created this page; often this is an email address. |
| **base** | If **true**, tells the Web client to set this Web page's location as the base for calling up any pages within this current page that have no leading http://. Otherwise, this option explicitly sets the base to assume for this document. |
| **bgcolor** | Indicates the color to use for this Web page's background. |
| **meta** | Provides information about the contents of this Web page. |
| **style** | Identifies the style sheet to use for this Web page. |
| **target** | Specifies the HTML target tag. |
| **title** | Provides the title information for this Web page. |

21. Perl Scripting

# Chapter 22

# Linux C Programming

| If you need an immediate solution to: | See page: |
| :--- | :--- |
| Installing The C Compiler | 647 |
| Compiling C Code With gcc | 647 |
| Debugging Code With gdb | 653 |
| Finding Resource-Hogging Sections With gprof | 656 |
| Installing The Build Manager | 658 |

## In Depth

One of the most popular programming languages used today is C. Although many computer buffs never need to understand the language or how to work with it, Linux administrators need to have a basic knowledge of how Linux deals with packages written in C. The RPM format has reduced the number of programs people have to compile for their system, but sometimes you won't be able to avoid compiling in C. Knowing a bit about how Linux works with C code can help immensely when you need to fix a package that will not compile properly on your system.

## Linux C Components

Several useful tools are available for C programmers under Linux. This chapter cannot possibly cover all of them, so only the most commonly available tools—mostly GNU tools—and most common tasks are presented here. Do not consider this chapter in any way to be a tutorial on C programming. If you are interested in learning more on this subject, try a book, such as *A Book On C*, Second Edition, by Al Kelley and Ira Pohl (The Benjamin/Cummings Publishing Company, Inc., 1990).

## The Compiler And Helpers

C is a compiled language, which means that you do not just run C code by itself. Instead, you run it through a processing program that converts your C program into machine language—raw bits and bytes. Compiled software typically runs faster than interpreted software, because the computer does not have to spend time converting the code into its own language.

The C—and C++—compiler used in Linux is often **gcc** (GNU C Compiler). When you utilize this program to build your code into a machine-executable format, it follows a particular progression of tasks, unless you tell it to do otherwise. This progression breaks down as follows:

- 1. *Preprocess the code.* This task involves locating the macros contained within the code and expanding them. These macros are typically declared with the `#define` command.
- 2. *Compile the code.* The actual job of converting the code to machine language.
- 3. *Assemble the code.* C code tends to be spread among a collection of files. This task merges the combined compiled code into one file.
- 4. *Link the code.* When you have external *object files*—a type of library containing code for external routines—called within your C code, pointers are added to these files at this stage.

Several helper programs also are available for Linux C programmers. One of these helpers is the GNU Debugger, **gdb**. If you are having trouble getting your C program (or one that you downloaded) to work properly, use this tool to step through the code and try to find the problem.

If you have a large program that is becoming a problem because it hogs up RAM and CPU time, then consider using the **gprof** tool. (See the Immediate Solutions section “Finding Resource-Hogging Sections With **gprof**” for more information about this tool.)

## The Libraries

When you are dealing with C programming, you often hear the term *library*. A library is a collection of precompiled subroutines that you or the users on your system can point to, rather than having to reinvent the wheel for common applications. You can find your overall libraries in the `/usr/lib` hierarchy. The ones that specifically come with **egcs**—the latest version of the GNU C Compiler—are in `/usr/lib/gcc-lib/i386-redhat-linux/egcs-version/include/`. This directory is full of `.h` (header) files. If you dig through these files, you will see a series of comments for what each routine in them does.

## The Build Manager

The tool that you are most likely to have to deal with is the build manager: **make**. Whenever you download source code, it almost always comes with a Makefile. This file automates the compilation process so you and other users do not have to figure out all the flags and other items necessary to get the program compiled with **gcc**. A Makefile is especially helpful for the many people who are Linux aficionados but not professional programmers.

A Makefile has a specific structure to it that can be represented as follows:

```
main target : requirements

instructions

target1 : requirements1

instructions1

...

targetN : requirementsN

instructionsN
```

As you can see, each of the line pairs—though there can be more than one set of instructions—follows the same format. It starts with the *target*, which is one of the following:

- A C object file (*file.o*).
- A **make** argument called a *make target*. This type of target enables you to type some of the standard installation instructions, such as **make install**, automating the entire process.
- The executable program itself.

The *requirements* refer to object files that have to be built before this particular target's instructions can be run. This is simply a space-separated list of object files. Finally, the *instructions* are typically simple *gcc* commands. A brief Makefile might be similar to the following:

```text
main : main.o sub1.o sub2.o
       gcc -o aill main.o sub1.o sub2.o
main.o : main.c
        gcc -c main.c
sub1.o : sub1.c
        gcc -c sub1.c
sub2.o : sub2.c
        gcc -c sub2.c
```

> **NOTE:** Manuals for all the GNU tools discussed here are available at [www.gnu.org/manual/manual.html](http://www.gnu.org/manual/manual.html).

## Immediate Solutions

### Installing The C Compiler

To install the C compiler, do the following:

1. Log in as root.
2. See whether you already have the C compiler in place by typing “ `rpm -q egcs` ”. If this package is located, you do not need to proceed.
3. Place the Red Hat CD-ROM into your CD-ROM drive.
4. Mount the CD-ROM by typing “ `mount /mnt/cdrom` ”.
5. Change to the packages directory by typing “ `cd /mnt/cdrom/RedHat/RPMS` ”.
6. Install the C compiler by typing “ `rpm -ivh egcs-1` ” and then pressing Tab to expand the file name. Press Enter.

> **NOTE:** You may be wondering why I said the compiler is **gcc** earlier in the chapter but you are installing the package *egcs*. The GNU C Compiler is officially maintained by EGCS as a way of merging two separate development projects. The latest information about this venture is available at [http://gcc.gnu.org](http://gcc.gnu.org).

### Compiling C Code With gcc

To compile C code with **gcc**, do the following:

1. Log in to the account that owns the code you want to work with.
2. Change to the directory containing the code by using the **cd** command.
3. Start by typing “ gcc ” at the command line. Do not press Enter yet.
4. Each of the four steps used by **gcc** has its own set of available command options. Choose the preprocessing options you want to use from Table 22.1. For this example, you want to go past the preprocessing point, so you will avoid the -E option. You also want to specify that your header files are in `/bin/cocode/headers`, and save out information that can help in building a Makefile. At this point, then, you have the following:

```
gcc -idirafter ~/bin/cocode/headers -MD
```
