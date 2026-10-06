
# Exercises 833

| | |
|---|---|
| ESCAPE U | Changes next word to all uppercase |
| ESCAPE . | Inserts last word from previous command line before current character |

# History Editing Commands (emacs)

| | |
|---|---|
| CONTROL-P | Moves to previous line in history file |
| CONTROL-N | Moves to next line in history file |
| ESCAPE< | Moves to first line in history file |
| ESCAPE> | Moves to last line in history file |
| CONTROL-R string | Search backward for string |

# Miscellaneous Commands (emacs)

| | |
|---|---|
| ESCAPE = | Lists pathnames that match current word (pathname listing) |
| ESCAPE ESCAPE | Completes current word to a unique or partial pathname (pathname completion) |
| ESCAPE* | Expands current word to all matching pathnames (pathname expansion) |
| CONTROL-U | Repeats next command four times |
| CONTROL-V | Displays the current version of the Z Shell |
| CONTROL-L | Redisplays the current line |

# Exercises

1. The dirname utility treats its argument as a pathname and writes to standard output the path prefix, that is, everything up to but not including the last component. Thus
`dirname a/b/c/d`
writes a/b/c to standard output. If path is a simple filename (has no / characters), dirname writes a . to standard output.

# 834 Chapter 15 The Z Shell and Advanced Shell Programming

Implement dirname as a Z Shell function. Make sure that it behaves sensibly when given such arguments as /.

- Implement the basename utility, which writes the last component of its pathname argument to standard output, as a Z Shell function. For example,
```zsh % basename a/b/c/d
writes d to standard output.
```

- The GNU/Linux basename utility has an optional second argument. If you type
```basename path suffix```
basename removes the suffix from path after removing the prefix. For example,
```zsh % basename src/shellfiles/prog.bash .bash
prog
zsh % basename src/shellfiles/prog.bash .c
bash
```
Add this feature to the function you write for exercise 2.

- Write a Z Shell function that takes a directory as an argument and writes to standard output the maximum of the lengths of all filenames in that directory. If the function's argument is not a directory name, write an error message to standard output and exit with nonzero status.

- Modify the function you wrote for exercise 4 to descend all subdirectories of the named directory recursively and to find the maximum length of any filename in hierarchy.

- Write a Z Shell function that lists the number of regular files, directories, block special files, character special files, FIFOs, and symbolic links in the working directory. Do this in two different ways:
  a Use the first letter of the output of ls -l to determine a file's type.
  b Use the file type condition tests of the [[ builtin to determine a file's type.

- The makers program (page 812) depends on the fact that find writes the pathname of a directory before writing the pathname of any files in that directory. Suppose this were not reliably true. Fix makers.

- Change makers (page 812) so that if any call to ci fails, the program continues (as it does now) but eventually exits with nonzero status.

- Modify the quiz program (page 816) so that the choices for a question are also randomly arranged.

# Advanced Exercises

10. In the makers (page 812) program, file descriptors 3 and 4 are opened; during the loop, output is directed to these descriptors. An alternative method would be simply to append the output each time it occurs, using; for example,

```
print "Cannot create $target" >>ERRS
```
rather than

```
print -u3 "Cannot create $target"
```
What is the difference? Why does it matter?

11. The check in makers (page 812) to prevent you from copying hierarchies on top of each other is simplistic. For example, if you are in your home directory, the call ./work/RCS will not detect that the source and target directories lie on the same path. Fix this check.

12. In principle, recursion is never necessary. It can always be replaced by an iterative construct, such as while or until. Rewrite makepath (page 809) as a nonrecursive function. Which version do you prefer?

13. Lists are commonly stored in environment variables by putting a colon (:) between each of the list elements.(The value of the PATH variable is a good example). You can add an element to such a list by concatenating the new element to the front of the list, as in

```
PATH=/opt/bin:$PATH
```
If the element you already is in the list, you now have two copies of it in the list. Write a Shell function, addenv takes two arguments:(1) the name of a shell variable and (2) a string to prepend to the list that is the value of the shell variable only if that string is not already an element of the list. For example, the call

```
addenv PATH /opt/bin
```
would add /opt/bin to PATH only if pathname is not already in PATH. Be that your solution works

# IN THIS CHAPTER

- Programming in C 837
- Using Shared Libraries 846
- make: Keeps a Set of Programs Current 849
- Debugging C Programs 857
- Threads 867
- System Calls 868
- Source Code Management 870

# Programming Tools 16

With its rich set of languages and development tools, the GNU/Linux operating system provides an outstanding environment for programming. C is one of the most popular system programming languages to use with GNU/Linux, in part because the operating system itself is written mostly in C. Using C, programmers can easily access system services using function libraries and system calls. In addition, variety of tools can make the development and maintenance of programs easier.

This chapter explains how to compile and link C programs. It introduces the GNU gdb debugger and tools that provide feedback about memory, disk, and CPU resources. It also covers some of the most useful software development tools: the make utility and two source code management systems, the Revision Control System (RCS) and the Concurrent Versions System (CVS). The make utility helps you keep track of which modules of a program have been updated and helps to ensure that when you compile a program, you use the latest versions of all program modules. Source code management systems track the versions of files involved in a project.

# Programming in C

One of the main reasons the GNU/Linux system provides an excellent C programming environment is that C programs can easily access the services of the operating system. The system calls—the routines that make operating system services

# Chapter 16 Programming Tools

available to programmers—can be called from C programs. The system calls provide services as creating files, reading from and writing to files, collecting information about processes, and sending signals to processes. When you write a program, you can use the system calls in the same way as you use ordinary C modules, or *functions*, that you have written. For more information, refer to "System Calls" on page 868.

A variety of libraries of functions has been developed to support programming in C. The libraries are collections of related functions that you can use as your own functions and the system calls. Many of the library functions access operating system services through the system calls, providing the services in ways that are more suited to typical programming tasks. Other library functions, such as the math library functions, serve special purposes.

the processes of writing and compiling C programs. However, it will not teach you to program in C. If you want to learn C, the many excellent texts on the market will help you. You can also look for tutorials on the Internet.

# Checking Your Compiler

The following command to see if you have access to the gcc compiler (www.gnu.org/software/gcc/gcc.html)!

```
$ gcc --version
bash: gcc: command not found
```

If you get a response other than version information, the compiler is not installed, or your PATH variable does not contain the necessary pathname (usually gcc is installed in /usr/bin). If you get version information from the gcc command, the GNU C compiler is installed.

Next, make sure that the compiler is functioning: create a file named Makefile with the following lines. The line that starts with gcc must be indented by a TAB, not SPACES:

```
$ cat Makefile
morning:morning.c	gcc -o morning morning.c
```

Next, create a source file named morning.c with the lines

-1. The C compiler in common use on GNU/Linux is GNU gcc, which comes as part of Red Hat. If it is on your system, you need to install the gcc*.rpm package.
