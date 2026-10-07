
size2 = size - 1;
string2 = (char *) malloc(size + 1);
for (i = 0; i < size; i++)
	string2[size2 - i] = string[i];
string2[size] = '\0';
printf("The string printed backward is %s\n", string2);
}

Indent does not change how the code compiles; it just changes how the source code looks. It makes the code more readable, which is always a good thing.

## gprof

gprof is a program that is installed in the /usr/bin directory on your Linux system. It allows you to profile programs that you write to determine where most of the execution time is being spent.

gprof will tell you how many times each function that your program uses is called and also the percentage of the total execution time the program spent in each function. This information can be very useful if you are trying to improve the performance of a program.

To use gprof on one of your programs, you must compile the program using the -pg gcc option. This causes the program to create a file called gmon.out each time it is executed. gprof uses the gmon.out file to generate the profile information.

After you run your program and it has created the gmon.out file, you can get its profile by entering the following command:

gprof <program_name>

The program_name parameter is the name of the program that created the gmon.out file.

### Tip

The profile data that gprof displays to the screen is quite large. If you want to examine this data, you should redirect gprof's output to a file.

## f2c and p2c

f2c and p2c are two source code conversion programs. f2c converts FORTRAN code into C code, and p2c converts Pascal code into C code. Both are included in the Linux installation when you install GCC.

If you have some code that has been written using either FORTRAN or Pascal that you want to rewrite in C, f2c and p2c can prove to be very useful programs. Both programs produce C code that can typically be compiled directly by GCC without any human intervention.

If you are converting small, straightforward FORTRAN or Pascal programs, you should be able to get away with using f2c or p2c without any options. If you are converting very large programs consisting of many files, you will probably have to use some of the command-line options which are provided by the conversion program that you are using.

To invoke f2c on a FORTRAN program, enter the following command:
`f2c my_fortranprog.f`

> **Tip**
> f2c requires that the program being converted has either a `.f` or a `.F` extension.

To convert a Pascal program to C, enter the following command:
`p2c my_pascalprogram.pas`

Both of these commands create C source code files that have the same name as the original file, except with a `.c` extension instead of `.f` or `.pas`.

For more information on the specific conversion options that are available with f2c or p2c, refer to their respective man pages.

## Summary

This chapter introduces the GNU C compiler and many of the options that you will typically use when you compile C code. It also introduces the concepts behind debugging code with the GNU debugger and illustrates the usefulness of some of the other C utility programs that are included on the Linux CD-ROM.

> **Tip**
> If you will be writing C code, the time that you spend learning how to use gdb and some of the other tools mentioned in this chapter will be more than worth the eventual time-saving that you will gain.

The next chapter will discuss many of the same topics, but with a focus on C++ development rather than C development. Instead of moving to C++, you can go to other chapters:

- Perl, a handy scripting language is discussed in Chapter 28, “Perl.”
- Tcl and Tk, useful for macros, is discussed in Chapter 29, “Introduction to Tcl and Tk.”
- The compilers available for Linux is discussed in Chapter 30, “Other Compilers.”
- Smalltalk is discussed in Chapter 31, “Smalltalk/X.”

# Chapter 27

## Programming in C++

by Rick McMullin

### In This Chapter

- What is C++? 486
- Classes of objects and methods 488
- GCC options 488
- Debugging and profiling options 490
- Debugging C++ applications 491
- Debugging virtual functions 492
- Debugging exception handlers 493
- Summary of gdb C++ specific commands 494
- GNU C++ class libraries 495

## What Is C++?

C++ is an object-oriented extension to the C programming language. It was developed at Bell Labs in the early 1980s and is quickly becoming the language of choice in the computer industry. Dozens of C++ compilers are available on the market today. The most common of these for PC-based systems are Borland C++, Microsoft's Visual C++, Zortech C++, and Watcom C++. These compilers compile MS-DOS and MS Windows applications, and some of them compile code to run on OS/2 and Windows NT, as well. In addition to the number of C++ compilers that are available on DOS-based machines, a great number are also based on other hardware architectures.

Most UNIX systems have C++ compilers available from the system vendor. Linux also comes with a C++ compiler. This is the GNU C++ compiler. The GNU C++ compiler is very closely related to the GNU C compiler (GCC). In fact, since Release 2.0 of GCC, the GNU C++ compiler has been integrated with GCC. Previous to Release 2.0 of GCC, the GNU C++ compiler was a separate program known as g++. One of the major enhancements in Release 2.0 of GCC was merging these two compilers.

GCC now incorporates a C compiler, a C++ compiler, and an Objective C compiler. You will still find the g++ executable on your system, but it is now a script file that calls GCC with all the standard C++ options.

## Why C++?

C++ and object-oriented programming (OOP) did not just happen. There were many fundamental reasons for the shift from structured programming to OOP. In the early days of computer programming, back when PDP-8s still roamed the earth in great numbers, there was a shift from machine language coding to assembler language coding. This was done because the computers of the day were a little more powerful than their predecessors. Programmers wanted to make their lives easier by moving some of the burden of programming onto the computer.

As the years went by and computers got even more powerful, new, higher-level languages started to appear. Examples of these languages are FORTRAN, COBOL, Pascal, and C. With these languages came a programming methodology known as structured programming. Structured programming helped to simplify the systems being designed by allowing programmers to break the problem into small pieces and then implement these pieces as functions or procedures in whatever language was being used.

The structured programming approach worked well for small to medium-sized software applications, but it started to fall apart as systems reached a certain size. OOP tried to solve some of the problems that structured programming was causing. It did this by extending some of the structured programming concepts and by introducing some of its own.

The main concepts that OOP focuses on are the following:

- Data encapsulation
- Inheritance
- Polymorphism

## Data Encapsulation

In structured programming, problems often arose wherever there was a data structure that was common to several different pieces of code. One piece of code could access that data without the other piece of code being aware that anything was happening.

Data encapsulation is a process of grouping common data together, storing it into a data type, and providing a consistent interface to that data. This ensures that no one can access that data without going through the user interface that has been defined for that data.

The biggest benefit that this kind of mechanism provides is that it protects code outside the code that is directly managing this data from being affected if the structure of the data changes. This greatly reduces the complexity of large software systems.

C++ implements data encapsulation through the use of classes.

## Inheritance

Inheritance is a form of code reuse in which you can inherit or use the data and behavior of other pieces of code. Inheritance is typically used only when a piece of software logically has many of the same characteristics as another piece of software, such as when one object is a specialization of another object.

Inheritance is implemented in C++ by allowing objects to be subclassed by other objects.

## Polymorphism

Polymorphism occurs when a language allows you to define functions that perform different operations on objects depending on their type. The true power of this lies in the fact that you can send a message to a base class and that message can be passed down to each of its subclasses and mean different things to each of them.

Polymorphism is implemented in C++ using virtual functions.
