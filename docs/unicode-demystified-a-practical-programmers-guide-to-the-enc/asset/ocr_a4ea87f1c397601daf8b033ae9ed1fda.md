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

+   1. The C compiler in common use on GNU/Linux is GNU gcc, which comes as part of Red Hat. If it is on your system, you need to install the gcc*.rpm package.