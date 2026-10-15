
```
scanf ("%f", &y);
printf ("x^y is: %6.3f\n", pow((double)x,(double)y));
return(0);
}
% gcc power.c
/tmp//ccnEwHNH.o: In function `main':
power_lib.c:(.text+0x73): undefined reference to `pow'
collect2: ld returned 1 exit status
% gcc power.c -lm -o power
% power
The program takes x and y from stdin and displays x^y.
Enter integer x: 9.82
Enter integer y: 2.3
x^y is: 191.362
%
```

## 17.5.3.3 Compiling C++ and Java Programs

You can use the gcc compiler to compile C++ programs as well. The file containing C++ source must have one of the following extensions: .C, .CPP, .cpp, .c++, or .cc.

Java source code is compiled (translated) into Java bytecode and is interpreted by the Java Virtual Machine (JVM), also known as the Java Interpreter. The Java compiler on our UNIX system is called javac, and the JVM is java. Thus, in order to run a Java program in a file, say Hello.java, we use the javac compiler to compile it. It produces the Java bytecode and stores it in the Hello.class file, which is interpreted with the java command, as shown in the following session.

```
% javac Hello.java
$ java Hello
Hello, world!
%
```

In the following in-chapter exercise, you will use the gcc and javac compiler commands to compile simple C, C++, and Java programs on your UNIX system and run them.

## EXERCISE 17.2

Create simple C, C++, and Java programs on your UNIX system. Compile and run them to appreciate the basic working of the two compilers (gcc and javac) and the Java Virtual Machine, java.

## 17.5.4 Handling Module-Based C Software

Most of the useful C software is divided into multiple source (.c and .h) files. This software structure has several advantages over a monolithic program stored in a single file. First, it leads to more modular software, which results in smaller program files that are

less time-consuming to edit, compile, test, and debug. It also allows recompilation of only those source files that are modified, rather than the entire software system. Furthermore, the multimodule structure supports information hiding, the key feature of object-oriented (OO) design and programming.

However, the multimodule implementation also has its disadvantages. First, you must know the files that comprise the entire system, the interdependencies of these files, and the files that have been modified since you created the last executable system. Also, when you are dealing with multimodule C software, compiling multiple files to create an executable sometimes becomes a nuisance because two long command lines have to be typed: one to create object files for all C source files, and the other to link the object files to create one executable file. An easy way out of this inconvenience is to create a simple shell script that does this work. The disadvantage of this technique is that, even if a single source file (or header file) is modified, all object files are recreated, most of them unnecessarily.

UNIX has a much more powerful tool called make, which allows you to manage the compilation of multiple modules into an executable. The make utility reads a specification file called the makefile, that describes how the modules of a software system depend on each other. The make utility uses this dependency specification in the makefile and the times when various components were modified, in order to minimize the amount of recompilation. This utility is very useful when your software system consists of tens of files and several executable programs. In such a system, remembering and keeping track of all header, source, object, and executable files can be a nightmare. The following is a brief description of the make utility.

### SYNTAX

```
make [-f makefile]
```

Purpose: Updates a file based on the dependency relationship stored in a makefile called makefile; the dependency relationship is specified in makefile in a particular format.

### Commonly used options/features:

- **-f** This option allows you to instruct make to read interdependency specification from any file; without this option, the file name is treated as makefile or Makefile.
- **-h** Display a brief description of all options.
- **-n** Do not run any makefile commands; just display them.
- **-s** Run in silent mode, without displaying any messages.

The make utility is based on interdependencies of files, target files that need to be built (e.g., executable or object file[s]), and commands that are to be executed to build the target files. These interdependencies, targets, and commands are specified in the makefile as make rules. The following is the syntax of a make rule.

### SYNTAX

```
target-list: dependency-list
Or
```
