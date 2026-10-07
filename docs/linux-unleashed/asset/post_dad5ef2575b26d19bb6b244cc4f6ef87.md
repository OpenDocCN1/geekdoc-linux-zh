
acm

acm is a multiplayer aerial combat game designed for the X window system that can be played in a LAN environment. Players engage in simulated air-to-air combat against one another using missiles and cannons.

Autoconf

Autoconf generates shell scripts that can automatically configure source code packages (such as those for GNU). Autoconf creates a script for a software package from a file that lists the operating system features that the package can utilize. Autoconf requires GNU m4 to generate the required macro calls for its operation.

bash

The shell called **bash** is an enhancement of the Bourne shell (thus the name, which stands for Bourne Again Shell). It offers many of the extensions found in **csh** and **ksh**. The **bash** shell also has job control, csh-style command history, and command-line editing with **Emacs** and **vi** modes built in. See Chapter 11, "**bash**."

bc

bc is an algebraic language that can be used interactively from a shell command line or with input files. GNU bc has a C-like syntax with several extensions, including multi-character variable names, an else statement, and full Boolean expressions. Unlike standard bc, GNU bc does not require the separate dc program, which is another GNU calculator utility.

BFD

The *Binary File Descriptor* (BFD) library allows a program that operates on object files (such as *ld* or *gdb*) to support many different formats efficiently. BFD provides a portable interface, so that only BFD needs to know the details of a particular format. One result is that all programs using BFD support formats such as *a.out* (default C executable) and COFF.

Binutils

Binutils includes a collection of development programs, including ar, c++filt, demangle, gprof, ld, nlmconv, objcopy, objdump, ranlib, size, strings, and strip.

Binutils Version 2 is completely rewritten to use the BFD library. The GNU linker ld emits source-line numbered error messages for multiply defined symbols and undefined references. nlmconv converts object files into Novell NetWare Loadable Modules (NLM). The objdump program can display data such as symbols from any file format understood by BFD.

Bison

Bison is an upwardly compatible replacement for the parser generator yacc. Bison takes a description of tokens in the form of a grammar and generates a parser in the form of a C program.

GNU C Compiler

Version 2 of the GNU C Compiler (gcc) supports three languages: C, C++, and Objective-C. The language selected depends on the source file suffix or a compiler option. The runtime support required by Objective-C programs is now distributed with gcc. The GNU C Compiler is a portable optimizing compiler that supports full ANSI C, traditional C, and GNU C extensions. GNU C has been extended to support features such as nested functions and nonlocal goto statements. Also, gcc can generate object files and debugging information in a variety of formats. See Chapter 27, "Programming in C," for more detailed information about C language support.

GNU C Library

The GNU C library supports ANSI C and adds some extensions of its own. For example, the GNU stdio library lets you define new kinds of streams and your own printf formats.

GNU C++ Library

The GNU C++ library (libg++) is an extensive collection of C++ classes, a new iostream library for input/output routines, and support tools for use with g++. Among the classes supported are multiple-precision integers and rational numbers, complex numbers, and arbitrary-length strings. Prototype files also exist for generating common container classes.

Calc

Calc is a desk calculator and mathematical tool that is used within GNU Emacs. Calc can be used as a basic calculator, but it provides additional features including choice of algebraic or Reverse Polish Notation (RPN), logarithmic functions, trigonometric and financial functions, complex numbers, vectors, matrices, dates, times, infinities, sets, algebraic simplification, differentiation, and integration.

GNU Chess

GNU Chess pits you against the computer in a full game of chess. It has regular-terminal, curses (a full-screen interface library for C), and X-terminal interfaces. GNU Chess implements many specialized features, including sophisticated heuristics that will challenge your best Bobby Fischer moves.

CLISP

CLISP is an implementation of Common Lisp, the list-processing language that is widely used in artificial-intelligence applications. CLISP includes an interpreter and a byte compiler and has user interfaces in English and German that can be chosen at compile time.

GNU Common Lisp

GNU Common Lisp (gcl) has a compiler and interpreter for Common Lisp. It is highly portable, extremely efficient, and has a source-level Lisp debugger for interpreted code. gcl also has profiling tools and an X11b interface.

cpio

cpio is a program that copies file archives to and from tape or disk. It can also be used to copy files into a larger archive file or to other directories.

CVS

The Concurrent Version System (CVS) manages software revision and release control in a multideveloper, multidirectory, multigroup environment. It works in conjunction with RCS, another source code control program.

dc

dc is an RPN calculator that can be used interactively or with input files.

DejaGnu

DejaGnu is a framework for writing scripts to test any program. It includes the embeddable scripting language Tc1 and its derivative expect, which runs scripts that can simulate user input.

Diffutils

The Diffutils package contains the file-comparison programs diff, diff3, sdiff, and cmp. GNU diff compares files showing line-by-line changes in several formats and is more efficient than its traditional version.

ecc

ecc is an error-correction checking program that uses the Reed-Solomon algorithm. It can correct a total of three byte errors in a block of 255 bytes and can detect more severe errors.

ed

ed is the standard line-based text editor.

Elisp

This is a small library of Emacs Lisp functions, including routines for using doubly linked lists.

GNU Emacs

GNU Emacs is the second implementation of this highly popular editor developed by Richard Stallman. It integrates Lisp for writing extensions and provides an interface to X. In addition to its own powerful command set, Emacs has extensions that emulate other popular editors such as vi and EDT (DEC’s VMS editor). For more information on Emacs, refer to Chapter 16, “Text Editors: vi and emacs.”

GNU Emacs 19

Emacs 19 is a richer version of the Emacs editor with extensive support for the X window system. It includes an interface to the X resource manager, has X toolkit support, has good RCS support, and includes many updated libraries. Emacs 19 from the FSF works equally well on character-based terminals as it does under X.

es

es is a shell based on rc that has an exception system and supports functions that return values other than just numbers. It works well interactively or in scripts, particularly because its quoting rules are simpler than the C and Bourne shells.

Fileutils

Fileutils is a GNU collection of standard (and not-so-standard) Linux file utilities, including chgrp, chmod, chown, cp, dd, df, dir, du, install, ln, ls, mkdir, mkfifo, mknode, mv, rmdir, touch, and vdir.

find

find is a program that can be used both interactively and in shell scripts to find files given certain criteria and then execute operations (such as rm) on them. This program includes xargs, which applies a command to a list of files.

finger

finger displays information about one or more Linux users. GNU finger supports a single host that can act as the finger server host in sites that have multiple hosts. This host collects information about who is logged into other hosts at that site. Thus, a query to any machine at another site returns complete information about any user at that site. Here's some sample output from a finger command:

```
# finger tparker@tpci.com
Login: tparker			Name: Tim Parker
Directory: /usr/tparker		Shell: /bin/sh
On since Sat Jun  6 11:33 on tty02, idle 51 days 21:22 (messages off)
On since Sun Jun  7 15:42 on ttyP0, idle 0:02
On since Sat Jun  6 11:33 on ttyP1, idle 21 days 10:01
Mail last read Tue Jun 16 18:38:48 1998
```
