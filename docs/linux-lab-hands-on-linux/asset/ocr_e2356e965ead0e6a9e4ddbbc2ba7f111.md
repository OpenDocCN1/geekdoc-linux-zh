# 26 C++ Programming Linux

# OBJECTIVES

+   Writing C++ source code in a text editor
+   Compiling source code
+   Executing source code

# REQUIREMENTS

+   A Standard PC (Intel or compatible) Configuration
+   Linux Distribution (such as Fedora 10) is installed in your PC

# CONCEPT

There are many different C and C++ compilers for Linux based operating system. Most of these are specific for a particular architecture and operating system. The GNU project has created a C/C++ compiler that has been ported to much different architecture. The g++ or g++ is the name of the compiler for the C or C++ compiler respectively. Due to the similarities between C and C++, the two commands actually call the same compiler with different default options.

You can create an executable program in a two step process. First you need to compile the source code to object code. Second, the object code is linked with other collections of object code (including system libraries) to form an executable file.

The GNU g++ compiler controls both the compilation phase and the linking phase of creating executable files.

# C++ Program in Linux

Use the following syntax to compile the program:

```
g++ -Wall -g -o [filename] [filename].cpp
```

Use the following syntax to run a program

```
./[filename]
```

# ▶ Program 1: Writing a program to print the following triangle:

```
*
* *
```