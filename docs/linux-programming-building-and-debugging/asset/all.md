![](images/00011.jpeg)

**Linux Programming: Building and Debugging**

**by Silviu Sosiade**

**Copyright @ 2016 by Silviu Sosiade. All rights reserved.**

No part of this publication may be reproduced, distributed or transmitted in any form or by any means, including photocopying, recording or other electronic or mechanical methods, or by any information storage retrieval system without the prior written permission of the publisher.

Although the author has made every effort to ensure that the information in this book was correct at publishing time, the author and publisher do not assume and hereby disclaim any liability to any party for any loss, damage, or disruption caused by errors or omissions, whether such errors or omissions result from negligence, accident, or any other cause.

# Table of contents

[Introduction](#part0000_split_003.html__toc76)

[Compilation vs. Interpretation](#part0000_split_004.html__toc97)

[Building an executable. Compilation and Linking](#part0000_split_005.html__toc108)

[GNU C/C++ Compiler - GCC](#part0000_split_006.html__toc128)

[Building a program from multiple source modules](#part0000_split_007.html__toc291)

[Make and Makefile](#part0000_split_008.html__toc380)

[Static Libraries](#part0000_split_009.html__toc600)

[Shared Libraries](#part0000_split_010.html__toc684)

[Debugging Linux programs](#part0000_split_011.html__toc810)

[Running under debugger](#part0000_split_012.html__toc868)

[Setting breakpoints](#part0000_split_013.html__toc953)

[Stepping through code](#part0000_split_014.html__toc1011)

[Setting watchpoints](#part0000_split_015.html__toc1043)

[Examining the content of variables](#part0000_split_016.html__toc1090)

[Setting variables and calling functions](#part0000_split_017.html__toc1221)

[Backtraceing and changing frames](#part0000_split_018.html__toc1279)

[Handling signals](#part0000_split_019.html__toc1413)

[Changing execution threads](#part0000_split_020.html__toc1750)

[Dealing with crashes](#part0000_split_021.html__toc1927)

[Running gdb with text user interface](#part0000_split_022.html__toc2061)

[Debugging memory access problems. Valgrind](#part0000_split_023.html__toc2112)

# Introduction

Linux has been around for a while. What started as an academic project of a very bright student represents now the main solution for many enterprise servers around the world. Also Linux operating system is winning over more and more followers as a solution for end user desktops. With the visual interfaces (KDE , GNOME) that were built specifically for Linux this operating system has become as easy to operate as Windows or MacOS and it is increasingly perceived less as a operating system for academic or programmers only.

Also if you use a setopbox for digital television or if you have an intelligent alarm at home, these devices are likely to use Linux OS as well. That's because Linux operating system has been ported to various types of processors or devices, becoming what we now call "embedded Linux".

Although with a very small market share, there are currently variants of mobile phones that use a version of Ubuntu Linux. Whether or not Linux will have a significant market share in the mobile phone market in the future, this remains to be seen. But the fact that there are mobile phones already using this operating system proves how versatile and flexible solution Linux has become these days.

The first program in Linux was written back in 1991\. This is nearly 25 years ago, which is a considerable age for the software market and and for the IT market in general. In the last 25 years we have seen many software products that had glory days and then replaced by other products. We have also seen once renowned companies that are now in the twilight of glory or out of business. Not the same thing happens with Linux. As time passes Linux becomes increasingly stronger. The secret of its “eternal youth” appears to be in using the GNU GPL license, a license that allows anyone to use this operating system for free. Moreover the use of this license has a much wider scope in what “free” means. This is the freedom to run, copy, distribute, study, change and improve the software. This aspect of “freedom” is attracting a large number of enthusiasts programmers from all over the world eager to contribute to the development of Linux. This ultimately creates a synergy hard to replicate for a software system whose code is not visible to the general public and that is developed and maintained only by a company or a group of companies.

One thing should be noted here if you do not know this already: Linux is not UNIX. But there is an obvious trend to use these terms interchangeably. And that is because there are many common aspects between Linux and UNIX, both in terms of usage as well as in term of programming.

Notable would also be the fact that there are many similarities between Android and Linux. Or between Mac OS and Linux. Although there are no compatibilities at the binary level (the Linux programs can not be executed on Mac OS or Android, and vice versa) there are however major similarities in terms of operating and programming using these operating systems. And this is understandable considering that the development of Android kernel started from an older version of Linux kernel, and various Linux kernel updates happening nowadays are regularly considered to be imported back into the Android kernel. Also Mac OS started from a variant of UNIX called BSD (Berkeley Software Distribution) that has many similarities with the Linux operating system. Therefore learning Linux opens up larger perspective for the Linux market itself as well as for other technologies present on the market at the moment.

Considering that Linux is gaining more and more ground, programming in Linux is no longer seen as being a niche job anymore. Increasingly more jobs are becoming available and are required for Linux programmers nowadays.

The Linux kernel was initially developed by using the C programming language. Since then, all the development and maintenance has been done using C. Similarly the majority of libraries and utility programs from a distribution of Linux are also written in C. At the application level, although it is possible to use other programming languages (Python , Java , Ruby ...), C and C++ still remain the preferred languages for many Linux programmers. The examples from this book are written in C/C++ therefore a basic understanding of the C language would help the reader to better understand the various topics presented in this book.

The book is based around the following topics:

· building a program, general consideration about compilation and linking.

· overview of GNU C/C++ compiler.

· how to build a program from multiple modules.

· static and dynamic libraries in Linux.

· debugging programs.

· detecting memory leaks.

The book is particularly useful for those who have programmed in other environments and operating systems before (Windows, for example) and now want to understand how to develop programs in Linux.

However by explaining the topics from this book in simple terms and by using a lot of examples I am hoping that this book will be a good starting point for anyone who wants to learn the basics for how to develop programs in Linux.

There are certainly many aspects which are not covered in this book. That's because the topics presented in this book are quite extensive and probably a book alone can be written for each section. But what I am trying achieve with this book is to provide a sufficient amount of information to allow the reader to understand the fundamental principles of creating programs in Linux and feel comfortable in trying something practical use cases based on knowledge gained from this book.       

# Compilation vs. Interpretation

If you bought this book, you probably have some interest and maybe an idea of how to develop computer programs. If I had told you that computer programming means writing endless sequences of 0s and 1s you would have likely abandoned any idea of exploring this topic any further! But this was the reality in the early days of computers when there was no distinction between "software" and "hardware" and the programs need to be written directly using the "machine language" – the low level instructions executed by the CPU.

The programmers from those days had to produce a number of punched cards containing the sequences of instructions that the microprocessor ultimately executed. In those conditions even writing trivial program required a considerable effort. Writing programs that allow automatic piloting of aircrafts would not have been possible without simplifying and making the programming of computers more effective.

There were two approaches to simplify the programming work: **interpreting** and **compiling**. Both approaches have in common writing programs using a more complex sequence of instructions than the CPU instructions set. With programming becoming more efficient, more functionality can be written with lesser lines of codes and writing more complex program became possible.

**Interpretation**: each line of code is interpreted and converted into an equivalent sequence of instructions executable by the CPU. These instructions are then executed. Then next line of code is interpreted and similarly executed. And program execution continues in this way until the last last line of the program is executed. Running a program in this way requires the use of an "interpreter" that allows the successive interpretation and execution of each line of the program.

Old programmers probably still remember BASIC, a programming language that is largely based on interpretation. The program interpretation however is present and very popular concept even today, especially for what programmers call "scripting programming” (shell scripting, perl, python, java script, etc ...)

**Compiling**: The program is first translated into another lower level intermediary language. The translated program can then either be executed directly or interpreted. The translation of high-level language into a lower level language is called **compilation**. For this, programmers need to use a "compiler" for that particular language. The C or C++ languages are examples of programming languages that use compilation.

Java is a programming language that uses of both of these concepts presented. A Java program is first "compiled" into Java byte code. This process is conducted by the Java compiler. Next, when a byte code program is executed every statement from the byte code program is subsequently "interpreted". The interpretation process is conducted by the Java virtual machine (JVM) that plays the interpreter role for byte code execution on different host machines.

In general, a compiled program is faster than an interpreted program. Therefore if the execution speed is critical then it is preferable to use a compiled language. On the other hand, the interpreted languages have the reputation to be simpler and easier to use, thus providing improved productivity.

# Building an executable. Compilation and Linking

Building (an executable) represents the process of going from source code to the actual executable. Although some programmers tend to colloquially call “build” as “compilation” in reality building an executable is performed in two distinct steps:

1 – **compilation**

2 – **linking**

**Compilation.** As concept, this is what I described in the previous chapter. Compiling C/C++ source code in Linux represents the process of translating the source code from the programming language and creating the “**object file**” which is the representation in machine language of the original source code.

For C/C++ language the compilation is typically done in two passes:

 **Step 1 – preprocessing**: this step involves pre-processing of the original source file by doing the following:

 a.– including the source code coming from #include directives

 b.– expanding the macros and substitution for #define directive

 c.– selecting parts of the original source code based on #if, #ifdef and #ifndef directives

![](images/00001.jpeg)
 **Step 2 – compilation itself**: this step represents the parsing of the plain code generated after pre-processing and creation of the object files.

I just mentioned that the output of the compilation is in format of machine language for. Then why we cannot execute directly the output of the compilation and we still need the linking stage?

There are two main reasons for this:

- an executable can be crested from multiple source code files (modules). Each source code file is individually translated into an equivalent object file. However only one file contains the definition of the main method, representing the main entry point for the executable. Thus we cannot execute a module which does not contain a main entry point. 

- the source code may contain references to functions defined in other modules or functions implemented in external libraries. The compilation itself does not deal with resolving these type of dependencies.

**Linking.** This is the process where all the object files are assembled together into what represents the final executable. Dependencies of external symbols are also resolved at this stage.

If a referenced function is defined in an external static library then the whole implementation of that function will be also added into the final executable.

![](images/00002.jpeg)

I briefly highlighted the role of the external libraries in building the final executable. An advantage of building an executables in two steps starts shaping up: the building process provides the ability to reuse various pre-compiled parts of code (libraries) across multiple programs and products. Another advantage is that the code can be structured in such a way so that parts of the code do not get recompiled every time the program is built. But more on libraries in a separate chapter.

# GNU C/C++ Compiler - GCC

There are several options for choosing a compiler for C/C++ programming languages, as you can see in the table below.

|  
**Compiler**

 |  
**Licence**

 |
|  
Ch

 |  
Freeware

 |
|  
[CodeWarrior](http://en.wikipedia.org/wiki/CodeWarrior)

 |  
Proprietary

 |
|  
[GCC](http://en.wikipedia.org/wiki/GNU_Compiler_Collection)

 |  
GPL

 |
|  
[Digital Mars](http://en.wikipedia.org/wiki/Digital_Mars)

 |  
Proprietary

 |
|  
[LabWindows/CVI](http://en.wikipedia.org/wiki/LabWindows/CVI)

 |  
Proprietary

 |
|  
[Lattice C](http://en.wikipedia.org/wiki/Lattice_C)

 |  
Proprietary

 |
|  
[lcc](http://en.wikipedia.org/wiki/LCC_(compiler))

 |  
Freeware

 |
|  
[Open Watcom](http://en.wikipedia.org/wiki/Open_Watcom)

 |  
Proprietary

 |
|  
[Portable C Compiler](http://en.wikipedia.org/wiki/Portable_C_Compiler)

 |  
BSD

 |
|  
[Smaller C](https://github.com/alexfru/SmallerC)

 |  
BSD

 |
|  
[Wind River (Diab) Compiler](http://en.wikipedia.org/wiki/Wind_River_Systems#Wind_River_.28Diab.29_Compiler)

 |  
Proprietary

 |
|  
[XL C](http://en.wikipedia.org/wiki/IBM_XL_C%2B%2B)

 |  
Proprietary

 |
|  
[HP aC++](http://en.wikipedia.org/wiki/HP_aC%2B%2B)

 |  
Proprietary

 |
|  
[Intel C++ Compiler](http://en.wikipedia.org/wiki/Intel_C%2B%2B_Compiler)

 |  
Proprietary

 |
|  
[VisualAge C++](http://en.wikipedia.org/wiki/IBM_VisualAge)

 |  
Proprietary

 |

For Linux however GCC (GNU Compiler Collection) represents by far the most popular option for building programs written in C/C++. Just think about the fact that GCC is the compiler used for compiling the Linux kernel itself. This speaks for itself about the robustness and reliability of this toolchain. And what makes it even better: it’s free!

Therefore GCC compiler will be used for building all the examples presented in this book.

If you are a Fedora, Red Hat or CentOS user then you can use the following command to install the GNU C/C++ compiler on your Linux machine:

*# sudo yum groupinstall 'Development Tools'*

Alternatively if you are Debian or Ubuntu user then you can use the following agt-get command for installation:

*# sudo apt-get install build-essential manpages-dev*

Assuming that the installation was successful then the following command should display the version of the newly installed compiler:

*$ gcc --version*

*gcc (GCC) 4.4.7 20120313 (Red Hat 4.4.7-11)*

*Copyright (C) 2010 Free Software Foundation, Inc.*

Lets use this compiler to compile the already famous “Hello World” program, presented by the parents of C language, Dennis Ritchie and Brian Kernighan.

Lets suppose that the following C program resides in a file named hello.c

*#include <stdio.h>*

*void main()*

*{*

 *printf("Hello world!\n");*

*}*

I can compile this C program by issuing the following command:

*$ gcc -g hello.c -o hello_c*

In the gcc command above I used “-o” option to specify the name of the generated executable (“hello_c”) and “-g” option to instruct the compiler to include debugging information in the output. It is a god practice to compile with debugging information during development so more functionality of the debugger can be used in order to fix possible issues.

The output of the command above is a Linux executable called “hello_c” that I can try to execute:

*$ ./hello_c*

*Hello world!*

The gcc command above oerforms the both steps building, compiling and linking, in one go.

If I want to build from source code and generate the object file file only, then I can use the following command:

*$ gcc -c hello.c*

The “-c” option stands for “compile” and instructs gcc to run only the pre-processor and compiler. The output of this command will be a “hello.o” object file located in the same folder. This object file can subsequently be linked using the following command:

*$ gcc hello.o -o hello_c*

Here gcc is smart enough to detect that an object file was passed in and execute only the linker. The generated output will be the same “hello_c” executable created in the first example but this time built by running the compilation and linker as two separate steps.

When required gcc can be run for pre-processesing only by using “-E” option:

*$ gcc -E hello.c*

After running the command above you will notice that the tiny hello.c program will increase significantly in size. This is because of #include <stdio.h> directive which will direct the pre-processor to include the entire content of theheader file alongside with all the other dependencies into the output of the pre processed C file..

It is also possible to stop the compiling after preprocessing and inspect the generated output.

Lets see how to build a C++ version of the “Hello World” example. And I will start from a hello.cpp file having the following content:

*#include "iostream"*

*int main(void)*

*{*

 *std::cout << "Hello world from C++.\n";*

 *return 0;*

*}*

I can build this with the following command line:

*$ g++ -g -Wall hello.cpp -o hello_cpp*

Where g++ is the GNU C++ compiler and “-g” and “-o” have the same meaning as in the gcc command line presented before.

Once the command above is successfully completed I can try to execute the generated executable:

*$ ./hello_cpp*

*Hello world from C++.*

This chapter was intended to give you a feeling of how to install and use GNU C/C++ compiler from command line. I can move to slightly more complex examples in the next sections of this book.

# Building a program from multiple source modules

There are very rare the cases when the content of a program is entirely located in a single source file. Good software development practices require using multiple source files for implementing various parts of the product.

Building a Linux program from C/C++ source code deals with several type of files:

- **Source files (*.cpp or *.c)** – text files that contain the main function implementation and the implementation for other functions or classes used by the program.

- **Header files (*.h)** – text files that contain functions or classes prototypes alongside with other processor statements. An example will be shown shortly in this chapter for source and header files.

- **Object files (*.o)** – the output of the compiler.

- **Binary files** – the executable, static libraries (*.a) or dynamic libraries (*.so). For now we can treat the libraries as being a prebuilt repository of object files which can be used in building other programs. I have two dedicated chapters later on in this book for building static and dynamic libraries.

Lets start with an example of a program that is created from three modules: **module1**, **module2** and **module3** respectively. The source code resides in the following files:

**main.c**

*#include "module1.h"*

*#include "module2.h"*

*#include "module3.h"*

*int main() {*

 *HelloModule1();*

 *HelloModule2();*

 *HelloModule3();*

 *return 0;*

*}*

**module1.h**

*#ifndef MODULE1_H_*

*#define MODULE1_H_*

*void HelloModule1();*

*#endif*

**module1.c**

*#include <stdio.h>*

*#include "module1.h"*

*void HelloModule1() {*

 *printf("Hello from module 1\n");*

*}*

**module2.h**

*#ifndef MODULE2_H_*

*#define MODULE2_H_*

*void HelloModule2();*

*#endif*

**module2.c**

*#include <stdio.h>*

*#include "module2.h"*

*void HelloModule2() {*

 *printf("Hello from module 2\n");*

*}*

**module3.h**

*#ifndef MODULE3_H_*

*#define MODULE3_H_*

*void HelloModule3();*

*#endif*

**module3.c**

*#include <stdio.h>*

*#include "module3.h"*

*void HelloModule3() {*

 *printf("Hello from module 3\n");*

*}*

Building a program from multiple sources typically involves the following steps:

- The source code files are “compiled” and object files are produced.

*$ gcc -c module1.c module2.c module3.c main.c*

*$ ls *.o*

*main.o module1.o module2.o module3.o*

- The object files are “linked” (or “archived”) producing the executable (or libraries respectively)

*$ gcc module1.o module2.o module3.o main.o -o hello*

*$ ./hello*

*Hello from module 1*

*Hello from module 2*

*Hello from module 3*

# Make and Makefile

We have just learnt from the previous chapter how to build a program from multiple source files. It seems easy and straight forward. But what if instead of three modules we have to deal with hundreds of source files (quite normal for large projects)?. Building a command line for gcc with so many files is obviously not an option. What do we do then?

The first thing that may spring to mind is to create a program or script that will attempt to automate the process of building the code and make this process easy and repeatable. The good news is that you do not have to write anything because such a program already exists. This is another GNU tool called “make”. The make program understands and executes different rules specified in an input file called “Makefile”. So while the make tool remains generic, the makefile contains the rules governing how a particular program has to be build.

I will start by presenting an example for a makefile that is functionally equivalent to the shell commands that I used to build the hello executable in the previous chapter. The goal of this example is to give a brief overview of the makefile syntax and usage.

To begin, lets assume I have the following files in my current working directory.

*$ ls*

*main.c Makefile module1.c module1.h module2.c module2.h module3.c module3.h*

The header and source files are the same files I used in the previous example. The content of the makefile file is the following:

*$ cat Makefile*

*module1.o: module1.c module1.h*

 *gcc -c module1.c*

*module2.o: module2.c module2.h*

 *gcc -c module2.c*

*module3.o: module3.c module3.h*

 *gcc -c module3.c*

*main.o: main.c*

 *gcc -c main.c*

*hello: main.o module1.o module2.o module3.o*

 *gcc module1.o module2.o module3.o main.o -o hello*

Before explaining the makefile syntax let me show you how I build the hello executable first:

*$ make hello*

*gcc -c main.c*

*gcc -c module1.c*

*gcc -c module2.c*

*gcc -c module3.c*

*gcc module1.o module2.o module3.o main.o -o hello*

Just by exploring the output of this command we can start getting some understanding about what make tool does. It compiles the source code first and then link the object files into the final executable.

If I list the content of the same directory once again I can see now the object files and executable being created.

*$ ls*

***hello*** *main.c **main.o** Makefile module1.c module1.h **module1.o** module2.c module2.h **module2.o** module3.c module3.h **module3.o***

If I run the executable I will get the same output as in my previous example when I built the executable from the command line:

*$ ./hello*

*Hello from module 1*

*Hello from module 2*

*Hello from module 3*

But what happens if I try to execute the make command once again?

*$ make hello*

*make: `hello' is up to date.*

It appears that make knows somehow that nothing has changed the since last build. So it does not recompile and link anything. Make detects this by checking the timestamps of the various files it uses or generates. If the binary artifacts are older that the source code then it does the compilation. Otherwise not.

To prove this, I am going to change the timestamp of module2.c

*$ ls -l module2**

*-rw-rw-r--. 1 ssosiade ssosiade 103 **Jul 30 07:29** module2.c*

*-rw-rw-r--. 1 ssosiade ssosiade 70 Jul 29 07:56 module2.h*

*-rw-rw-r--. 1 ssosiade ssosiade 1512 **Jul 30 07:30** module2.o*

*$ touch module2.c*

*$ ls -l module2**

*-rw-rw-r--. 1 ssosiade ssosiade 103 **Jul 30 07:32** module2.c*

*-rw-rw-r--. 1 ssosiade ssosiade 70 Jul 29 07:56 module2.h*

*-rw-rw-r--. 1 ssosiade ssosiade 1512 **Jul 30 07:30** module2.o*

Now module2.c appears to be newer that module2.o. If I run the “make hello” again then module2.c only will be recompiled again and the executable will be recreated.

*$ make hello*

*gcc -c module2.c*

*gcc module1.o module2.o module3.o main.o -o hello*

This feature reduces the total time of the build by building only parts of the system which are affected by the latest code changes since the last build. This feature really makes a significant difference especially for large systems where a build from scratch (clean builds) could take hours .

Lets go back now to the makefile and explain how make utility understands from the content of the makefile what to do and what to build.

The key element in a makefile is represented by a **rule**. A make rule starts with a **target** and has the following format:

*target: dependencies*

*<TAB> command1*

*<TAB> command2*

*<TAB> commandN*

Please note that <TAB> must be the TAB character and it cannot be replaced by a sequence of blanks in order to achieve the same level of indentation. This is one of the most common errors in makefiles. A message like:

*“Makefile:11: *** missing separator (did you mean TAB instead of 8 spaces?). Stop.”*

would indicate for example that a TAB is missing on line 11.

When a target is invoked make will process the dependencies first followed by the sequential execution of all the commands specified in the target body (“command1”, “command2”...”commandN”).

A target can be invoked in one of the following ways:

1) From the command line by using “make <target>”

2) As part of the processing of another target

To understand this better lets analyze some of the rules presented in the makefile from my example:

*module3.o: module3.c module3.h*

 *gcc -c module3.c*

For the above rule the “target” (module3.o) depends on module3.c and module3.h. When this target is invoked the make tool will try to determine if module3.o exists and whether its timestamp is newer that module3.c and module3.h respectively. If any of these is not true then make will invoke the command “gcc -c module3.c”

Target “module3.o” can be independently invoked from the command line as follows:

*$ make module3.o*

*gcc -c module3.c*

Lets explore this rule:

*hello: main.o module1.o module2.o module3.o*

 *gcc module1.o module2.o module3.o main.o -o hello*

In this rule, “hello” target is dependent on the following list of targets: “main.o module1.o module2.o module3.o”. Before executing the gcc command make will first need to invoke module1.o target, followed by module2.o, and so on. A complex target will result in a “dependency tree” that needs to be processed.

This is for example the dependency tree for “hello” target from my example:

![](images/00003.jpeg)

The command(s) associated with a target can be any Linux shell commands. There is no restriction on what shell commands can be used in makefiles. Therefore makefile targets can be written that so that files can be moved around or deleted or to do any other operations that you would normally expect to see in a regular shell script. In reality, many makefiles contains targets such as “make install” or “make deploy” which has nothing to do with compiling and linking C/C++ code.

For example, below is a “clean” target whose purpose is to delete the executable and all the objects files previously created by “make hello” command.

*clean:*

 *rm -rf hello *.o*

Thus the following command “**make clean hello**” represents a way to force make to rebuild everything from scratch:

*$ make clean hello*

*rm -rf hello *.o*

*gcc -c main.c*

*gcc -c module1.c*

*gcc -c module2.c*

*gcc -c module3.c*

*gcc module1.o module2.o module3.o main.o -o hello*

The make tool contains what is called **“builtin rules”** (or **“default rules”**). What do you think will happen if I remove the target “module1.o” from my makefile and try to invoke “make module1.o” from the command line? You would probably be tempted to say that this command will fail. Well, this is not quite the case:

*$ make module1.o*

*cc -c -o module1.o module1.c*

Why is this? First let’s not forget that make was written particularly for controlling and automating the build process. To make the work easy some default rules for a number of popular programming languages (C, C++, Fortran, Modula-2, and so on…) have been integrated into make tool. These rules act like “fallback rules” if no other matching rules are found in the makefile. Therefore based on the *.o suffix the make tool is able to determine that the target is referring to a C (or C++) object file so it must look for a module1.c (or module1.cpp) file in the current folder.

I am personally not convinced how useful these builtin rules are. Built in rules may cause subtle issues sometimes and very hard to detect. For instance the builtin rules for C use the standard C compiler “cc” whereas the makefile uses GNU C compiler “gcc”. Some people probably do find these rules useful but I am personally in favor of having full control on how programs are built so I prefer to either disable built in rules (make --no-builtin-rules) or override them in my makefiles.

The overriding of the built in rules is possible by using what make tool understands by “**pattern based rules**”. Here is how the previous makefile will look like by using a single rule that specifies the all the object files (*.o) should be created from a corresponding *.c file and by using “gcc” compiler.

*$ cat Makefile*

*%.o: %.c*

 *gcc -c $^*

*hello: main.o module1.o module2.o module3.o*

 *gcc module1.o module2.o module3.o main.o -o hello*

*clean:*

 *rm -rf hello *.o*

One could easily notice that the use of pattern based rules makes the makefiles look tidier and more compact.

Before going any further I need to provide you a quick explanation regarding the pattern based rule written above. “%.o: %.c” says that for any given <file name>.o the make tool must search for a <file name.c> file in the current folder. To some extent this is similar to using “*” wildcard in Linux but with one constrain: it must be an exact match for the file name for both object and source file.

What does “$^” from the last makefile mean? This refers to an internal variable which expands to the name of the prerequisite (<file name.c>. Similarly “$@” contains the name of the target (<file name.o>).

I just mentioned that “$^” refers to a “**variable**”. Yes, we can use variables when writing makefiles.

I will give you a quick example to understand how variables can be useful in makefiles. Let's assume that I want to change the compiler, so instead of using gcc complier I want to use a different compiler. In all the makefiles that I presented so far if I want to change GNU compiler then I need to change the makefiles in several places where “gcc” string is present. What if I use a variable .lets name it CC, to store the name of the compiler and have this variable used in the rest of the makefile instead of hardcoding the name of the compiler? Now I will only to change the “value” of this variable and this change will be propagated everywhere in the makefile. See the following makefile for example:

*$ cat Makefile*

*CC=gcc*

*%.o: %.c*

 *${CC} -c $^*

*hello: main.o module1.o module2.o module3.o*

 *${CC} module1.o module2.o module3.o main.o -o hello*

*clean:*

 *rm -rf hello *.o*

Similarly, the compiler parameters represents something that may need to be changed quite often during the development of a program or even after. This represents another good example where makefile variables could be useful:

*$ cat Makefile*

*CC=gcc*

*CCFLAGS=-Wall -g*

*%.o: %.c*

 *${CC} ${CCFLAGS} -c $^*

*hello: main.o module1.o module2.o module3.o*

 *${CC} module1.o module2.o module3.o main.o -o hello*

*clean:*

 *rm -rf hello *.o*

Makefile also supports conditional statements (if-then-else). I am going to refer to another common use case in order to introduce the conditional statements for makefile. I would like to expand the makefile from my previous example so that I can invoke it as “make DEBUG=true” from the command line when I want to build the program with debugging information (-g).

Here is how this can be implemented by using makefile conditional statements:

*$ cat Makefile*

*CC=gcc*

*ifeq ($(DEBUG),true)*

*CCFLAGS=-Wall -g*

*else*

*CCFLAGS=-Wall*

*endif*

*hello: main.o module1.o module2.o module3.o*

 *${CC} module1.o module2.o module3.o main.o -o hello*

*%.o: %.c*

 *${CC} ${CCFLAGS} -c $^*

*clean:*

 *rm -rf hello *.o*

The last topic regarding makefile syntax that I would to discuss are **functions**. A function call in terms of makefile syntax resembles to some extent a variable reference.

*$(function arguments)*

You may or may not have a variable on the left hand side storing the return value of the function:

*var := $(function arguments)*

Below is an example of a function call that stores the names of all the files with extension txt in the variable ALL_TEXT_FILES. This is done by invoking the “shell” function and passing “ls *.tst” as input argument.

*ALL_TEXT_FILES:=$(shell ls *.txt)*

Make has a sizable number of functions that can be usefull in different situations. The list is far too long to be covered in this book. But I strongly recommend bookmark and to check the official make documentation ([https://www.gnu.org/software/make/manual](https://www.gnu.org/software/make/manual)) to learn about various functions being available. Using functions allows achieving greater flexibility therefore functions are extensively used in almost any makefile used in building slightly more complex software products.

It's probably the time to see an example of using functions in the makefile that I have been gradually refining in this chapter. One limitation of the last makefile I presented is that every time when I will be adding a new C module I will also need to manually update the dependency list for the hello target. I would like automate this somehow and be able just to drop a C source file in that folder and have the makefile capable of figuring out which object files are required to build the executable.

This is where functions can help. See in the makefile below how to implement this:

*SOURCE_FILES = $(wildcard *.c)*

*OBJECT_FILES = $(SOURCE_FILES:.c=.o)*

*CC=gcc*

*ALL_TEXT_FILES:=$(shell ls *.txt)*

*ifeq ($(DEBUG),true)*

*CCFLAGS=-Wall -g*

*else*

*CCFLAGS=-Wall*

*endif*

*hello: ${OBJECT_FILES}*

 *${CC} ${OBJECT_FILES} -o $@*

*%.o: %.c*

 *${CC} ${CCFLAGS} -c $^*

*clean:*

 *echo ${ALL_TEXT_FILES}*

 *rm -rf hello *.o*

This concludes the brief presentation of the make tool and makefile syntax. The purpose of this chapter is to give you a good starting point in working with makefiles in order to build your Linux programs.

When you will need to explore the build system for a large system you will likely see an entire collection of makefiles and that build system may look a bit overwhelming and hard to understand. But you should not worry, reading complex makefiles represents a challenge even for seasoned Linux programmers. However all the complexity is built on top of the simple concepts that I presented in this book and with a little time and patience you will be able to understand what the build system does and gradually be able to maintain and update it. 

# Static Libraries

In numerous cases exactly the same functions are used by several programs. Therefore it will make sense to “package” these functions as Linux libraries and use them for different programs as required. 

Linux has two types of libraries:

- **Static libraries** (the scope of this chapter)

- **Shared libraries** (presented in the next chapter)

Static libraries are files containing a collection of multiple object files. Static libraries in Linux are also known as “archive” and this is the reason because static library files have the extension *.a.

The tool used for creating and updating library files is called “ar” and has the following syntax:

*ar options archive-file object-file…*

The most common options for the ar tool are:

-d - delete file(s) from the archive

-m - move file(s) in the archive

-p - print file(s) found in the archive

-q - quick append files(s) to the archive

-r - replace exiting or insert new file(s) into the archive

-t - display content of archive

-x -extract file(s) from archive

For example here is how I can create a Linux static library (libhello.a) using the objects files module1.o, module2.o and module3.o respectively.

*$ ar r libhello.a module1.o module2.o module3.o*

*ar: creating libhello.a*

*$ ls*

*libhello.a main.o module1.o module2.o module3.o*

*$ file libhello.a*

*libhello.a: current ar archive*

Now I can use this library instead of using the object files to link it with main module and create the hello executable:

*$ gcc -g -o hello main.o libhello.a*

*$ ls*

*hello libhello.a main.o module1.o module2.o module3.o*

*$ ./hello*

*Hello from module 1*

*Hello from module 2*

*Hello from module 3*

Another way to build the same executable using this library is to place the library in a location used by the linker (e.g /usr/lib) and use –l gcc switch:

*$ gcc -g -o hello main.o –lhello*

If I want to use the library from the current directory (.) or from another directory then I can simply extend the linker search path by using –L gcc switch as follows:

*$ gcc -g -o hello main.o -L. –lhello*

Or:

*$ gcc -g -o hello main.o -L`pwd` -lhello*

Below is the makefile the last example, updated to build the static library and link the main executable against it.

*$ cat Makefile*

*LIB_SOURCE_FILES = $(wildcard module*.c)*

*LIB_OBJECT_FILES = $(LIB_SOURCE_FILES:.c=.o)*

*CC=gcc*

*AR=ar*

*LNK_OPTS=-L. -lhello*

*ifeq ($(DEBUG),true)*

*CCFLAGS=-Wall -g*

*else*

*CCFLAGS=-Wall*

*endif*

*hello: main.o libhello.a*

 *${CC} main.o -o $@ ${LNK_OPTS}*

*libhello.a: ${LIB_OBJECT_FILES}*

 *${AR} r $@ ${LIB_OBJECT_FILES}*

*%.o: %.c*

 *${CC} ${CCFLAGS} -c $^*

*clean:*

 *rm -rf hello libhello.a *.o*

And this is the example of to invoke make using the above makefile:

*$ make*

*gcc -Wall -c main.c*

*gcc -Wall -c module1.c*

*gcc -Wall -c module2.c*

*gcc -Wall -c module3.c*

*ar r libhello.a module1.o module2.o module3.o*

*ar: creating libhello.a*

*gcc main.o -o hello -L. –lhello*

One drawback with using static libraries is that when a static library is updated then all the programs using it needs to be relinked in order to get in the latest changes from the library.

# Shared Libraries

Although simple enough to use, static libraries have a distinctive disadvantage: sections of code used from libraries is replicated into each of the executables and therefore the system will have multiple copies of the same binary data on disk as well as in memory when those programs are executed.

For instance if we had two executables hello1 and hello2 linked against same static library then the executable will have approximately the following binary layout:

![](images/00004.jpeg)

Shared libraries address this shortcoming by using only one version of the common code for all the executables. The way this is achieved is depicted in the following figure:

![](images/00005.jpeg)

And here is how this works:

1\. The first program that needs the shared library loads the library into memory at the same time with the program.

2\. The second, third,.. etc program that need the same library will reuse the library already loaded into memory. A reference count for the number of programs using that library is maintained.

3\. When a program finishes the reference count is decremented.

4\. When the reference count reaches zero, this means that no active programs are using that library and the library is unloaded from memory.

In order to achieve the above functionality, the linking process responsibilities is now shared with the program loader. When building the executable the linker will only insert the symbols for the what is used from the shared libraries. The program loader will actually resolve at run time the exact addresses for those symbols for the library loaded in memory. This step is called “**symbol relocation**” or “**runtime linking**” and the part of the program loader responsible for this task is called **dynamic linker**. As a matter of fact the dynamic linker itself is a Linux shared library (/lib/ld-linux*.so)

Because of symbol relocation, loading a program that uses shared objects will take longer than a similar program using static libraries.

A shared library can be loaded anywhere in the Linux virtual memory. A code that can be loaded anywhere in memory is called **position-independent code**. Therefore when generating shared objects the compiler needs be instructed to generate position-independent code. -fPIC is option for gcc to generate such output. See this in the example below:

*$ gcc -c -fPIC module1.c module2.c module3.c*

Linking the shared-object requires using “-shared” option:

*$ gcc -shared -o libhello.so module1.o module2.o module3.o*

A libhello.so file is created in the current directory after the above command is executed.

The makefile used to build the hello executable using libhello.so shared library is presented below:

*$ cat Makefile*

*LIB_SOURCE_FILES = $(wildcard module*.c)*

*LIB_OBJECT_FILES = $(LIB_SOURCE_FILES:.c=.o)*

*CC=gcc*

*LNK_OPTS=libhello.so*

*SOLNKFLAGS=-shared -o*

*ifeq ($(DEBUG),true)*

*CCFLAGS=-Wall -g*

*SOCCFLAGS=-Wall -g -c -fPIC*

*else*

*CCFLAGS=-Wall*

*SOCCFLAGS=-Wall -c -fPIC*

*endif*

*hello: main.o libhello.so*

 *${CC} main.o -o $@ ${LNK_OPTS}*

*libhello.so: ${LIB_OBJECT_FILES}*

 *${CC} ${SOLNKFLAGS} $@ ${LIB_OBJECT_FILES}*

*${LIB_OBJECT_FILES}: ${LIB_SOURCE_FILES}*

 *${CC} ${SOCCFLAGS} $^*

*%.o: %.c*

 *${CC} ${CCFLAGS} -c $^*

*clean:*

 *rm -rf hello libhello.so *.o*

If I try to execute the hello executable generated by using the above makefile I get the following output:

*$ ./hello*

*./hello: error while loading shared libraries: libhello.so: cannot open shared object file: No such file or directory*

What is wrong or missing here? The failure is at the point where the dynamic linker is trying to load the libhello.so into memory but it fails to find it. The is happening because the dynamic linker is looking for shared libraries in some predefined paths (for example: /lib, /usr/lib, /usr/local/lib…etc) and my shared library is located in the current directory which is not part of the dynamic loader search path. I have few options to fix this:

**Option 1:** To copy the shared object into a directory which is included in the dynamic loader search path.

**Option 2:** To use the LD_LIBRARY_PATH to append extra directories to the dynamic loader search path

Example:

*$ LD_LIBRARY_PATH=. ./hello*

*Hello from module 1*

*Hello from module 2*

*Hello from module 3*

**Option 3**: To use ldconfig to append extra directories to the dynamic loader search path

Example:

*edit /etc/ld.so.conf to include the additional path(s) I need (current working directory is required for this example)*

*$ sudo ldconfig*

*$ ./hello*

*Hello from module 1*

*Hello from module 2*

*Hello from module 3*

Please note that super user permissions are required in order to be able to edit /etc/ld.so.conf as well as to be allowed to execute ldconfig command. One can use ldconf –v in order to see where the dynamic linker is searching for shared libraries and what libraries are found. “man ldconfig” will provide detailed information on how to use this tool and other options available for this tool.

There is a way to find all the dynamic dependencies of a particular program by using a tool called ldd (“list dynamic dependencies”). Running this tool against my hello executable will produce the following output:

*$ ldd hello*

 *linux-vdso.so.1 => (0x00007fff9d5fb000)*

 *libhello.so => /home/samples_book/dynamic_lib/libhello.so (0x00007fb06a752000)*

 *libc.so.6 => /lib64/libc.so.6 (0x0000003c87c00000)*

 */lib64/ld-linux-x86-64.so.2 (0x0000003c87800000)*

I can see from this output that apart from depending on my shared library (libhello.so) the hello program also requires the C library (libc.so), the Linux dynamic loader (ld-linux*.so) and a library used to make system calls into kernel space (linux-vdso.so). These latest three libraries are included in almost any Linux executable that is build to use shared libraries.

Using shared libraries removes the need of relinking the executables when the library is changed or updated. For example I should be able to update libhello.so to a newer version (libhello.so.2) and all the programs depending on this shared library can use the latest version without the need to rebuild or relink any executables.

However, as we can see from the output of ldd, hello executable depends strictly on a binary called “libhello.so”. Therefore could the renaming the shared library break the executable? And the answer here is yes! Then how does Linux solve this problem?

The solution is to use a “wrapper library” (**soname**) instead of the actual name of the shared library. Sonames represents a level of indirection that permits an executable to use a different version of a shared library instead of the one that was used during linking. This allows updating the library without the need to relink the executable, because the executable will continue to reference the soname library.

This is how I can modify the command line in order to use the soname:

*$gcc -shared -Wl,-soname,libhellowrapper.o -o libhello.so module1.o module2.o module3.o*

If I list the content of the folder I see that only libhello.so has been generated. However the major difference in this case is that the new shared libraries also contains the soname library internally.

*$ strings libhello.so | grep libhellowrapper.so*

*libhellowrapper.so*

Linking using the shared object with soname is basically the same as using any shared object:

*$gcc -g -Wall -o hello main.c libhello.so*

The difference however is that the linker will recognize the soname embedded in the shared library and will use this one instead.

![](images/00006.jpeg)

By using “ldd” I can see now that hello binary is referencing the soname wrapper library instead of the shared library itself:

*$ ldd hello*

 *linux-vdso.so.1 => (0x00007fffaffff000)*

 *libhellowrapper.so => not found*

 *libc.so.6 => /lib64/libc.so.6 (0x0000003c87c00000)*

 */lib64/ld-linux-x86-64.so.2 (0x0000003c87800000)*

On disk soname must be a softlink pointing to the library itself. Therefor the last step in order to use the soname is to create this softlink:

*$ ln -s libhello.so libhellowrapper.so*

*$ ls -lrt libhellowrapper.so*

*lrwxrwxrwx. 1 ssosiade ssosiade 11 Aug 5 06:50 libhellowrapper.so -> libhello.so*

With all of these in place I can now try to run the executable and I am expect to see the same output as first time I executed the hello executable because nothing was changed in the source code, just the way the code built:

*$ ./hello*

*./hello: error while loading shared libraries: libhellowrapper.so: cannot open shared object file: No such file or directory*

*$ LD_LIBRARY_PATH=. ./hello*

*Hello from module 1*

*Hello from module 2*

*Hello from module 3*

However now if I want to change the shared library I will only need to change the softlink in order to point to the new binary, and that's it. No rebuild or relink are necessary.

For example if a newer libhello.so.2 is available I can just simply swap the old one with this by doing:

*$ ln -s libhello.so.2 libhellowrapper.so*

And the hello will execute now using the new library.

# Debugging Linux programs

One of the most useful tools that comes with the GNU toolchain is gdb (GNU Debugger). This tool canprovide invaluable assistance when trying to understand why a program is crashing or why a program is not not doing what it was designed to do.

I am going to need a slightly more complex C program than “hello world” in order to to explain the main features of the gdb tool. For this reason I am going to use a non recursive version of a program that displays the Fibonacci series for a given number of terms.

This is the listing of this program:

*$ cat fibonacci.c*

*#include<stdio.h>*

*int main()*

*{*

 *int n, first = 0, second = 1, next, i;*

 *printf("Number of terms: \n");*

 *scanf("%d",&n);*

 *for ( i = 0 ; i < n ; i++ )*

 *{*

 *if ( i <= 1 )*

 *next = i;*

 *else*

 *{*

 *next = first + second;*

 *first = second;*

 *second = next;*

 *}*

 *printf("%d\n",next);*

 *}*

 *return 0;*

*}*

And here is a quick reminder on how I can build this program by using gcc:

*$ gcc –g fibonacci.c -o fibonacci*

*$ ./fibonacci*

*Number of terms:*

*6*

*0*

*1*

*1*

*2*

*3*

*5*

**Note**: Compiling using –g (“with debugging symbols”) is very important in order to make use of the most debugging capabilities of the gdb tool.

Lets see some examples on how I can use this program in order to explore the following features of the GNU debugger:

· Running program under debugger

· Setting breakpoints

· Stepping through code

· Setting watchpoints

· Examining the content of variables

· Setting variables and calling functions

· Backtraceing and changing frames

· Handling signals

· Changing execution threads

· Dealing with crashes

· Running gdb with text user interface

If you have ever used any debugging tool before then you will probably see many similar features available in gdb. If this is the first time using a debugger then don't worry. I wrote this part of the book assuming that is first time you are using a command line debugging tool.

## Running under debugger

In order to debug a program, this program has to be executed within the debugger environment. There are several ways to do this:

a) **Option 1:** Run gdb with the program passed in as parameter:

*$ gdb ./fibonacci*

*GNU gdb (GDB) Red Hat Enterprise Linux (7.2-64.el6_5.2)*

*Copyright (C) 2010 Free Software Foundation, Inc.*

*License GPLv3+: GNU GPL version 3 or later <http://gnu.org/licenses/gpl.html>*

*This is free software: you are free to change and redistribute it.*

*There is NO WARRANTY, to the extent permitted by law. Type "show copying"*

*and "show warranty" for details.*

*This GDB was configured as "x86_64-redhat-linux-gnu".*

*For bug reporting instructions, please see:*

*<http://www.gnu.org/software/gdb/bugs/>...*

*Reading symbols from /books/gdb/fibonacci...(no debugging symbols found)...done.*

Once the program is loaded I can run the executable using command “r” (or “run”)

*(gdb) run*

*Starting program: /home/ssosiade/tmp_books/gdb/fibonacci*

*Number of terms:*

*2*

*0*

*1*

b) **Option 2:** Run “gdb” first and then load and execute the program from the debugger command line:

*$ gdb*

*GNU gdb (GDB) Red Hat Enterprise Linux (7.2-64.el6_5.2)*

*Copyright (C) 2010 Free Software Foundation, Inc.*

*License GPLv3+: GNU GPL version 3 or later <http://gnu.org/licenses/gpl.html>*

*This is free software: you are free to change and redistribute it.*

*There is NO WARRANTY, to the extent permitted by law. Type "show copying"*

*and "show warranty" for details.*

*This GDB was configured as "x86_64-redhat-linux-gnu".*

*For bug reporting instructions, please see:*

*<http://www.gnu.org/software/gdb/bugs/>.*

*(gdb) exec-file ./fibonacci*

*(gdb) r*

*Starting program: /books/gdb/fibonacci*

*Number of terms:*

c) **Option 3**: Attach the debugger to a running program

In order to attach gdb to a program already running, the PID of the program must be known first. I can find the PID of my fibonacci program using the following Linux command:

*$ ps -a | grep fibonacci*

*38532 pts/0 00:00:00 fibonacci*

Now by having the PID of this process (38532) I can proceed with attaching the debugger to this process:

*$ gdb attach 38532*

*GNU gdb (GDB) Red Hat Enterprise Linux (7.2-64.el6_5.2)*

*Copyright (C) 2010 Free Software Foundation, Inc.*

*License GPLv3+: GNU GPL version 3 or later <http://gnu.org/licenses/gpl.html>*

*This is free software: you are free to change and redistribute it.*

*There is NO WARRANTY, to the extent permitted by law. Type "show copying"*

*and "show warranty" for details.*

*This GDB was configured as "x86_64-redhat-linux-gnu".*

*For bug reporting instructions, please see:*

*<http://www.gnu.org/software/gdb/bugs/>...*

*attach: No such file or directory.*

*Attaching to process 38532*

*Reading symbols from /books/gdb/fibonacci...done.*

*Reading symbols from /lib64/libc.so.6...(no debugging symbols found)...done.*

*Loaded symbols for /lib64/libc.so.6*

*Reading symbols from /lib64/ld-linux-x86-64.so.2...(no debugging symbols found)...done.*

*Loaded symbols for /lib64/ld-linux-x86-64.so.2*

*0x0000003c87cdb520 in __write_nocancel () from /lib64/libc.so.6*

*(gdb) list*

*1 #include<stdio.h>*

*2*

*3 int main()*

*4 {*

*5 int n, first = 0, second = 1, next, i;*

*6*

*7 printf("Number of terms: \n");*

*8 scanf("%d",&n);*

*9*

*10 for ( i = 0 ; i < n ; i++ )*

I can use “**q**” (“**quit**”) command in order to quit the debugging session at any time:

*(gdb) q*

*A debugging session is active.*

 *Inferior 1 [process 38532] will be detached.*

*Quit anyway? (y or n) y*

*Detaching from program: /books/gdb/fibonacci, process 38532*

## Setting breakpoints

Breakpoints are used to stop the execution of the program at a specific location in the program. The gdb command for setting breakpoints is **“b” (“break”)** and it has multiple syntaxes:

**b module:line** - sets a breakpoint at a specific line in a specific module

**b symbol** - sets a breakpoint at a specific symbol

**b line** – sets a breakpoint at a particular line in the current module

**b +lines** – sets a breakpoint a number of lines after the current execution point

**b -lines** – sets a breakpoint a number of lines before the current execution point

**b module:function** – sets a breakpoint for a particular function in a different module

**b** – sets a breakpoint at the next line

**b address** – sets the breakpoint at a particular address

Here is an example on how to set a breakpoint at line number 10 in fibonacci.c file:

*(gdb) b fibonacci.c:10*

*Breakpoint 1 at 0x4005ad: file fibonacci.c, line 10.*

And here is an example on how to set a breakpoint when the first call to “printf” is made:

*(gdb) b printf*

*Breakpoint 2 at 0x400450*

The following command can be used to see all the breakpoints in use:

*(gdb) info break*

*Num Type Disp Enb Address What*

*1 breakpoint keep y 0x00000000004005ad in main at fibonacci.c:10*

*2 breakpoint keep y 0x0000000000400450 <printf@plt>*

Breakpoints can be deleted or disabled. A disabled breakpoint behaves similarly as a deleted breakpoint. The only difference is that a disabled breakpoint can be reused (reenabled) at some later point in time if needed.

The gdb commands “**enable**” and “**disable**” can be used in order to enable or disable a breakpoint:

*(gdb) disable 1*

*(gdb) info break*

*Num Type    Disp Enb Address What*

*1 breakpoint keep n 0x00000000004005ad in main at fibonacci.c:10*

*2 breakpoint keep y 0x0000000000400450 <printf@plt>*

*(gdb) enable 1*

*(gdb) info break*

*Num Type Disp Enb Address     What*

*1 breakpoint keep y 0x00000000004005ad in main at fibonacci.c:10*

*2 breakpoint keep y 0x0000000000400450 <printf@plt>*

Similarly to delete a break point “**delete**” gdb command can be used. Here is for example how to delete the second breakpoint from the list above:

*(gdb) delete 2*

*(gdb) info break*

*Num Type Disp Enb Address What*

*1 breakpoint keep y 0x00000000004005ad in main at fibonacci.c:10*

Once I have the breakpoints set I can start executing the program. The execution of the program will stop as soon as the first breakpoint is hit:

*(gdb) r*

*Starting program: /books/gdb/fibonacci*

*Number of terms:*

*5*

*Breakpoint 1, main () at fibonacci.c:10*

*10 for ( i = 0 ; i < n ; i++ )*

## Stepping through code

Once execution of the program is stopped I can choose to continue executing the program “step-by-step”. Step by step execution is particularly useful for the following cases:

· to see if the program follows the flow that it was intended by design

· to follow the values of variables for each instruction of the program.

The commands for step by step debugging are **“s” (“step”)** and **“n” (“next”)**. The difference between them is the following: “step” continues the execution until the next line of program from the same module is hit. This means that if execution of the current line requires calling functions from different modules these calls will be fully executed and the debugger will not be stepping into these calls.

When stepping into the nested calls is required then “next” command can be be used. This command will make the debugger to stop at the next line of code in the program regardless of whether this is in the current module or not.

Below is an example about how I can step through the code starting from the line 10 of the program:

*(gdb) b 10*

*Breakpoint 1 at 0x400626: file fibonacci.c, line 10.*

*(gdb) r*

*Starting program: /books/linux_building/fibonacci*

*Number of terms:*

*4*

*Breakpoint 1, main () at fibonacci.c:10*

*10 for ( i = 0 ; i < n ; i++ )*

*(gdb) n*

*12 if ( i <= 1 )*

*(gdb) s*

*13 next = i;*

*(gdb) n*

*20 printf("%d\n",next);*

*(gdb) s*

*0*

*10 for ( i = 0 ; i < n ; i++ )*

*(gdb) s*

*12 if ( i <= 1 )*

*(gdb) s                                                                                                                                         *

*13 next = i;                                                                                 *

## Setting watchpoints

Watchpoints are similar to breakpoints to some extent. The main difference is that watchpoints are set on variables instead location of the code. Therefore instead of instructing the debugger “to stop at line 10 in module foo.c” by using a watchpoint we can instruct the debugger to stop “when value of variable y has changed” or “when value of variable x is equal to 5”.

Before seeing an example with watchpoints I must tell you that the compiler can sometimes do some optimizations regarding how to handle the automatic variables. The compiler may decide for instance to store variables in the CPU registers instead of memory. This will make the access to those variables significantly faster, but the trade-off here is that we cannot use watchpoints because there are no symbols generated for these variables when CPU registers are used.

Typical gdb message for this case is: *“No symbol "foo" in current context.”*

A way to avoid using registers for holding program variables is to force the compiler to perform no optimization (using -O0) as in the following example:

*$ gcc -O0 -g fibonacci.c -o fibonacci*

Now I can be sure that each variable has a corresponding symbol and I can use any variable for setting watchpoints.

Below is an example on how I can set a watchpoint to stop the execution of the program every time the variable “next” is modified.

*(gdb) watch next*

*Hardware watchpoint 2: next*

All the watchpoints can be listed alongside with the breakpoints:

*(gdb) info break*

*Num Type Disp Enb Address What*

*2 **hw watchpoint** keep y next*

Also watchpoints can be enabled, disabled or deleted in the similar way as I did with the breakpoints by using gdb commands “enable”, “disable” and “delete” respectively.

If I run the program using the above watchpoint the debugger execution will be as follows:

*(gdb) c*

*Continuing.*

*Number of terms:*

*4*

*0*

*Hardware watchpoint 2: next*

*Old value = 0*

*New value = 1*

*0x00000000004005c2 in main () at fibonacci.c:13*

*13 next = i;*

We can see from the output above that the program has stopped at line 13 in the program while executing the following statement: next = i;

What if for example I want to stop the program only when the value of the counter “i” becomes 5\. Here is how I can do this:

*(gdb) watch i=5*

*Hardware watchpoint 2: i=5*

*(gdb) c*

*Continuing.*

*Number of terms:*

*10*

*Hardware watchpoint 2: i=5*

*Old value = <unreadable>*

***New value = 5***

*0x00000000004005b4 in main () at fibonacci.c:10*

*10 for ( i = 0 ; i < n ; i++ )*

## Examining the content of variables

How could I check for the previous example that the program actually stops when it should be?

How can we inspect the content of the variable i and ensure that has the value of 5 when the execution of the program stops?

The content of the variables can be inspected by using “**print**” command.

*(gdb) print i*

*$1 = 5*

So I can see that indeed the watchpoint was triggered as expected and the variable i has the value of 5 when the program execution stopped. I can continue to poke around to see the values of the other variables:

*(gdb) print first*

*$5 = 0*

*(gdb) print second*

*$6 = 1*

*(gdb) print n*

*$7 = 10*

“print” allows specifying several output formats:

x - print as integer in hexadecimal.

d - print as integer in signed decimal.

u - print as integer in unsigned decimal.

o - print as integer in octal.

t - print as integer in binary.

a - print as an address

c - print as a character constant.

f - print using typical floating point syntax.

Here are some example for displaying the variable n using each of the above formats:

*(gdb) print/x n*

*$8 = 0xa*

*(gdb)*

*$9 = 0xa*

*(gdb)*

*$10 = 0xa*

*(gdb)*

*$11 = 0xa*

*(gdb) print/x n*

*$12 = 0xa*

*(gdb) print/d n*

*$13 = 10*

*(gdb) print/u n*

*$14 = 10*

*(gdb) print/o n*

*$15 = 012*

*(gdb) print/t n*

*$16 = 1010*

*(gdb) print/a n*

*$17 = 0xa*

*(gdb) print/c n*

*$18 = 10 '\n'*

*(gdb) print/f n*

*$19 = 1.40129846e-44*

If at any point in the debugging session I am not sure what type a variable is I can use “**whatis**” command for this purpose:

*(gdb) whatis i*

*type = int*

*(gdb) whatis next*

*type = int*

If I need to monitor continuously certain variables then I could use “**display**” command that will automatically print variables for each of the subsequent gdb commands.

Below is an example of how I can check the content of the following program variables: i, first, second and next for each step of the program:

*(gdb) display n*

*1: n = 0*

*(gdb) display first*

*2: first = -7568*

*(gdb) display second*

*3: second = 32767*

*(gdb) display i*

*4: i = 0*

*(gdb) watch i*

*Hardware watchpoint 2: i*

*(gdb) c*

*Continuing.*

*Number of terms:*

*4*

*0*

*Hardware watchpoint 2: i*

*Old value = 0*

*New value = 1*

*0x00000000004005f7 in main () at fibonacci.c:10*

*10 for ( i = 0 ; i < n ; i++ )*

*4: i = 1*

*3: second = 1*

*2: first = 0*

*1: n = 4*

*(gdb) c*

*Continuing.*

*1*

*Hardware watchpoint 2: i*

*Old value = 1*

*New value = 2*

*0x00000000004005f7 in main () at fibonacci.c:10*

*10 for ( i = 0 ; i < n ; i++ )*

*4: i = 2*

*3: second = 1*

*2: first = 0*

*1: n = 4*

*(gdb) c*

*Continuing.*

*1*

*Hardware watchpoint 2: i*

*Old value = 2*

*New value = 3*

*0x00000000004005f7 in main () at fibonacci.c:10*

*10 for ( i = 0 ; i < n ; i++ )*

*4: i = 3*

*3: second = 1*

*2: first = 1*

*1: n = 4*

*(gdb) c*

*Continuing.*

*2*

*Hardware watchpoint 2: i*

*Old value = 3*

*New value = 4*

*0x00000000004005f7 in main () at fibonacci.c:10*

*10 for ( i = 0 ; i < n ; i++ )*

*4: i = 4*

*3: second = 2*

*2: first = 1*

*1: n = 4*

*(gdb) c*

*Continuing.*

I can turn off monitoring a variable by using “**undisplay**” command.

## Setting variables and calling functions

Sometimes we may need to change the flow or the data for a program during the debugging session. This means changing values of variables “on the fly” or forcing the program to execute an instruction other than the one that is supposed to be executed next.

How could we force the debugger to alter the value of a variable? This can be done by using debugger “**set**” command as in the example below:

*(gdb) print i*

*$1 = 0*

*(gdb) set var i=5*

*(gdb) print i*

*$2 = 5*

To demonstrate calling functions from within gdb I need to slightly alter the example used so far in order to add a new function (foo) and use it to be invoked from debugger during a debugging session. See the modified program below:

*#include <stdio.h>*

***void foo() {***

 ***printf("foo called!\n");***

***}***

*int main()*

*{*

 *int n, first = 0, second = 1, next, i;*

 *printf("Number of terms: \n");*

 *scanf("%d",&n);*

 *for ( i = 0 ; i < n ; i++ )*

 *{*

 *if ( i <= 1 )*

 *next = i;*

 *else*

 *{*

 *next = first + second;*

 *first = second;*

 *second = next;*

 *}*

 *printf("%d\n",next);*

 *}*

 *return 0;*

*}*

Please observe the function foo in the context of the program. This function is not called from anywhere in program. Normally this function will never get executed. Below is an example on how I can force the call of this function from debugger just before executing line 11:

*(gdb) b 9*

*Breakpoint 1 at 0x40058c: file fibonacci.c, line 9.*

*(gdb) r*

*Starting program: /books/gdb/fibonacci*

*Breakpoint 1, main () at fibonacci.c:9*

*9 int n, first = 0, second = 1, next, i;*

*(**gdb) call foo()***

***foo called!***

*(gdb) n*

*11 printf("Number of terms: \n");*

Another common use cases needed in altering the flow of the program is forcing to return from a function from wherever the execution is without executing the rest of the function body. The “**return**” command can be used for this purpose. The “return” gdb command has the following syntax and depends on whether the function being executed was designed to return a value or not:

*return*

or:

*return value*

## Backtraceing and changing frames

The level of nested calls for many programs can go very deep. That means that function A is currently executed because it was called from function B. And function B was executed because it was called from function C. And so on… functions calls are stacked on top of each other with every new call to a function being made.

A new function call is represented by a new “frame” (or “stack frame”). This frame typically contains the return address, the function local variables and eventually the function parameters.

![](images/00007.jpeg)

The current stack frame can be inspected with the debugger using:

*(gdb) info frame*

*Stack level 0, frame at 0x7ffd0ed4a1d0:*

*rip = 0x400540 in functionC (crashy.c:5); saved rip 0x400556*

*called by frame at 0x7ffd0ed4a1e0*

*source language c.*

*Arglist at 0x7ffd0ed4a1c0, args:*

* Locals at 0x7ffd0ed4a1c0, Previous frame's sp is 0x7ffd0ed4a1d0*

*Saved registers:*

 *rbp at 0x7ffd0ed4a1c0, rip at 0x7ffd0ed4a1c8*

For every program in execution there is a stack of call frames that can be inspected with the debugger. This stack starts with the main entry point of the program (main()) and adds a new frame when a new call is made and removes a frame when the execution of a function is completed.

I need another simple program to be able to provide a meaningful example for stack inspection and navigation feature provided by gdb. Below is a program where functionA() calls functionB(). Then functionB() calls functionC(). And finally functionC() calls functionD().

![](images/00008.jpeg)

*#include <stdio.h>*

*void functionA();*

*void functionB();*

*void functionC();*

*void functionD();*

*void functionA() {*

 *int a;*

 *a = 1;*

 *printf("functionA called!\n");*

 *functionB();*

*}*

*void functionB() {*

 *int b;*

 *b = 2;*

 *printf("functionB called!\n");*

 *functionC();*

*}*

*void functionC() {*

 *int c;*

 *c = 3;*

 *printf("functionC called!\n");*

 *functionD();*

*}*

*void functionD() {*

 *int d;*

 *d = 4;*

 *printf("functionD called!\n");*

*}*

*int main()*

*{*

 *functionA();*

 *return 0;*

*}*

Lets build and execute the above program without using the debugger first:

*$ gcc -O0 -g backtrace_demo.c -o backtrace_demo*

*$ ./backtrace_demo*

*functionA called!*

*functionB called!*

*functionC called!*

*functionD called!*

Now I am going to run the same program and set a breakpoint when the line 36: printf("functionD called!\n"); is executed. We already know how to set breakpoints:

*$ gdb ./backtrace_demo*

*GNU gdb (GDB) Red Hat Enterprise Linux (7.2-64.el6_5.2)*

*Copyright (C) 2010 Free Software Foundation, Inc.*

*License GPLv3+: GNU GPL version 3 or later <http://gnu.org/licenses/gpl.html>*

*Reading symbols from /books/gdb/backtrace_demo...done.*

*(gdb) b backtrace_demo.c:36*

*Breakpoint 1 at 0x400542: file backtrace_demo.c, line 36.*

*(gdb) r*

*Starting program: /books/gdb/backtrace_demo*

*functionA called!*

*functionB called!*

*functionC called!*

*Breakpoint 1, functionD () at backtrace_demo.c:36*

*36 printf("functionD called!\n");*

I can see from the output that the program called functions A, B and C respectively. But how could I have known this if the program did not have this output?

gbd provides “**backtrace**” command for this purpose:

*(gdb) backtrace*

*#0 functionD () at backtrace_demo.c:36*

*#1 0x0000000000400531 in functionC () at backtrace_demo.c:29*

*#2 0x000000000040050c in functionB () at backtrace_demo.c:21*

*#3 0x00000000004004e7 in functionA () at backtrace_demo.c:13*

*#4 0x000000000040055c in main () at backtrace_demo.c:42*

Frame #0 contains the top of the calling stack and I can see that gdb is just about to execute line 36 from functionD inside backtrace_demo.c module. But no surprise here as this is precisely the place where I set my breakpoint.

In the context of the last frame I can inspect the content of any local variables if present. functionD has variable d so lets check its value:

*(gdb) print d*

*$1 = 4*

I can inspect the values of all local variables in “one go” by using:

*(gdb) info local*

*d = 4*

What about local variable “c” from functionC?

*(gdb) print c*

*No symbol "c" in current context.*

Bad luck? Not at all! I can still access this variable by qualifying it with the function name as follows:

*(gdb) print functionC::c*

*$2 = 3*

I can also change the current frame and navigate between frames by using “**up**” and “**down**” gdb commands:

*(gdb) up*

*#2 0x000000000040050c in functionB () at backtrace_demo.c:21*

*21 functionC();*

*(gdb) info local*

*b = 2*

*(gdb) down*

*#1 0x0000000000400531 in functionC () at backtrace_demo.c:29*

*29 functionD();*

*(gdb) info local*

*c = 3*

The following represents the call stack after functionB() and functionC() return:

![](images/00009.jpeg)

*(gdb) backtrace*

*#0 functionA () at backtrace_demo.c:14*

*#1 0x000000000040055c in main () at backtrace_demo.c:42*

The abilities to inspect any call frame and navigate through the the call stack are very powerful debugging features for debugging certain categories of problems dealing with the flow of program execution. 

## Handling signals

Linux signals are asynchronous notification sent from one process to one or more processes in order to inform that a particular event has occurred.

The receiving processes may handle or ignore the incoming signal. All signals can de ignored except one (SIGKILL). SIGKILL is the signal that Linux uses to forcefully close programs that misbehave, or when Linux needs to free up some memory or forcefully close running applications during shutdown operation.

Below is a list of all the Linux signals and a short description for each of them:

| **Sig #** | **Sig name** | **Note** |
| 1 | SIGHUP | If a process is being run from terminal and that terminal is closed then the process receives this signal. |
| 2 | SIGINT | The process was “interrupted”. This happens when Control+C is pressed.. |
| 3 | SIGQUIT |   |
| 4 | SIGILL | Illegal instruction. The program contained some machine code the CPU cannot execute. |
| 5 | SIGTRAP | This signal is used mainly from within debuggers and program tracers. gdb is using this signal under the hood to implement breakpoints or step-by-step execution. |
| 6 | SIGABRT | The program called the abort() function. This is an emergency stop other than the normal termination of the program. |
| 7 | SIGBUS | This is be caused by an attempt was made to access memory incorrectly. |
| 8 | SIGFPE | This is be caused by by a floating point exception that happened in the program. |
| 9 | SIGKILL | The process was explicitly killed by somebody intending to forcefully stop the program. |
| 10 | SIGUSR1 | Available for the programmers to use it for any custom purposes. |
| 11 | SIGSEGV | This is be caused by an attempt to access memory not allocated to the process. |
| 12 | SIGUSR2 | Available for the programmers to use it for any custom purposes. |
| 13 | SIGPIPE | If a process is producing output that is being fed into another process that consume it via a pipe (“producer &#124; consumer”) and the consumer dies then the producer is sent this signal. |
| 14 | SIGALRM | A process can request a “wake up call” from the operating system at some time in the future by calling the alarm() function. |
| 15 | SIGTERM | The process was explicitly killed by a user or a process intending to kill program. |
| 16 |   |   |
| 17 | SIGCHLD | The process had previously created one or more child processes with the fork() function. One or more of these processes has since died. |
| 18 | SIGCONT | If a process has been paused by sending it SIGSTOP then sending SIGCONT to the process wakes it up again (“continues” it) |
| 19 | SIGSTOP | A process that receives SIGSTOP signal is paused by the operating system. All its state is preserved ready for it to be restarted (by SIGCONT). |
| 20 | SIGTSTP | Pretty much the same as SIGSTOP. This is the signal sent when the user hits Control+Z on the terminal.  |
| 21 | SIGTTIN | The operating system sends this signal to a backgrounded process when it tries to read input from its terminal. |
| 22 | SIGTTOU | The operating system sends this signal to a background process when it tries to write output to its terminal. |
| 23 | SIGURG | The operating system sends this signal to a process using a network connection when “urgent” out of band data is sent to it. |
| 24 | SIGXCPU | The operating system sends this signal to a process that has exceeded its CPU limit.  |
| 25 | SIGXFSZ | The operating system sends this signal to a process that has tried to create a file above the file size limit.  |
| 26 | SIGVTALRM | This is very similar to SIGALRM, but while SIGALRM is sent after a certain amount of real time has passed, SIGVTALRM is sent after a certain amount of time has been spent running the process. |
| 27 | SIGPROF | This is also very similar to SIGALRM and SIGVTALRM, but while SIGALRM is sent after a certain amount of real time has passed, SIGPROF is sent after a certain amount of time has been spent running the process and running system code on behalf of the process. |
| 28 | SIGWINCH | A process used to be sent this signal when one of its windows was resized. |
| 29 | SIGIO | A process can receive this signal when there is some input ready for it to process or an output channel has become ready for writing. |
| 30 | SIGPWR | A signal sent to processes by a power management service to indicate that power has switched to a short term emergency power supply. . |
| 31 | SIGSYS | Unused |

gdb is capable of detecting the occurrence of any signal during a debug session. Upon receiving a signal gdb can do any of the following actions depending upon your debugging strategy:

· **Stop**: interrupt the execution of the program and present the gdb prompt

· **Print**: display information about the occurrence on the signal on the standard output

· **Pass to program**: relay the signal to the debugged program thus allowing the program to handle the signal as it would do it in normal circumstances.

In order to see what actions gdb is configured to do for each of signals the “**info signals**” gdb command can be used:  

*(gdb) info signals*

*Signal Stop Print Pass to program Description*

*SIGHUP Yes Yes Yes Hangup*

*SIGINT Yes Yes No Interrupt*

*SIGQUIT Yes Yes Yes Quit*

*SIGILL Yes Yes Yes      Illegal instruction*

*SIGTRAP Yes Yes No Trace/breakpoint trap*

*SIGABRT Yes Yes Yes Aborted*

*SIGEMT Yes Yes Yes Emulation trap*

*SIGFPE Yes Yes Yes       Arithmetic exception*

*SIGKILL Yes Yes Yes Killed*

*...*

If I want to see information only about a single signal then I would simply need to add the signal name at the end of the “info signals” gdb command as in the following example:

*(gdb) info signals SIGTERM*

*Signal Stop Print Pass to program Description*

*SIGTERM Yes Yes Yes Terminated*

gdb allows controlling the handling of signals by using “**handle**” command. Here is for example how I can disable all the three actions for the SIGTERM above:

*(gdb) handle SIGTERM nostop noprint ignore*

*Signal Stop Print Pass to program Description*

*SIGTERM No No No Terminated*

*(gdb) info signals SIGTERM*

*Signal     Stop Print Pass to program Description*

***SIGTERM No No No Terminated***

To undo the last command and revert back to the default SIGTERM handling I can do the following:

*(gdb) handle SIGTERM stop print noignore*

*Signal       Stop Print Pass to program Description*

***SIGTERM Yes Yes Yes Terminated***

gdb has also the ability to send a signal to the debugged program. This can be done by either using “**signal**” or “**queue-signal**” commands. There is a very slight difference between these two commands:

· “**signal *signal***”: resumes the program and the signal is delivered immediately.

· “**queue-signal *signal***”: delivers the signal as soon as the program is resumed.

## Changing execution threads

Non trivial Linux programs typically consist of multiple execution threads. Therefore a powerful debugging tool for Linux must be able to handle multithreaded programs as well. And gdb ticks this box.

To understand the multithreading capabilities for gdb lets consider a multithreaded version of the fibonnaci.c program that does the calculation of three Fibonacci series in parallel. See the program in the listing below. Please note the error handling has not been provided in order to keep this example small:

*1: #include <stdio.h>*

*2: #include <pthread.h>*

*3:*

*4: #define NUM_THREADS 3*

*5: void* fibonacci(void *arg)*

*6: {*

*7: int n, first = 0, second = 1, next, i;*

*8:*

*9: n = (int)arg;*

*10:*

*11: for ( i = 0 ; i < n ; i++ )*

*12: {*

*13: if ( i <= 1 )*

*14: next = i;*

*15: else*

*16: {*

*17: next = first + second;*

*18: first = second;*

*19: second = next;*

*20: }*

*21: sleep(5);*

*22: }*

*23:*

*24: printf("Fib(%d)=%d\n", n, next);*

*25: return NULL;*

*26:}*

*27:*

*28: int main()*

*29: {*

*30: pthread_t tid[NUM_THREADS];*

*31: int n[NUM_THREADS];*

*32: int i;*

*33:*

*34: /* read input data */*

*35: for ( i = 0; i < NUM_THREADS; i++ )*

*36: {*

*37: printf("Thread %d: Number of terms: \n", i);*

*38: scanf("%d",&n[i]);*

*39: }*

*40:*

*41: /* start computation threads */*

*42: for ( i = 0; i < NUM_THREADS; i++ )*

*43: {*

*44: pthread_create(&(tid[i]), NULL, &fibonacci, (void*)n[i]);*

*45: }*

*46:*

*47: /* wait for threads to finish */*

*48: for ( i = 0; i < NUM_THREADS; i++ )*

*49: {*

*50: pthread_join(tid[i], NULL);*

*51: }*

*52: printf("Game over!\n");*

*53: }*

The program can be built from the command line with the following command: 

*$ gcc -g fibonacci_threads.c -lpthread -o fibonacci_threads*

The output of the command above is an executable called: fibonacci_threads. Lets see how this program executes before exploring it with the debugger:

*$ ./fibonacci_threads*

*Thread 0: Number of terms:*

*6*

*Thread 1: Number of terms:*

*4*

*Thread 2: Number of terms:*

*2*

*Fib(2)=1*

*Fib(4)=2*

*Fib(6)=5*

*Game over!*

Now it's time to see an example how to run this program under gdb. Every command I presented so far in this book applies to multithreaded programs as well. Therefore starting the program under debugger and setting a breakpoint at line 48 must be something that you should be familiar with by now:

*$ gdb fibonacci_threads*

*GNU gdb (GDB) Red Hat Enterprise Linux 7.6.1-51.el7*

*Copyright (C) 2013 Free Software Foundation, Inc.*

*License GPLv3+: GNU GPL version 3 or later <*[*http://gnu.org/licenses/gpl.html*](http://gnu.org/licenses/gpl.html)*>*

*....*

*Reading symbols from /home/books/fibonacci_threads...done.*

*(gdb) b 48*

*Breakpoint 1 at 0x4008bc: file fibonacci_threads.c, line 48.*

I can now execute the program until the breakpoint is hit:

*(gdb) r*

*Starting program: /home/books/fibonacci_threads*

*[Thread debugging using libthread_db enabled]*

*Using host libthread_db library "/lib64/libthread_db.so.1".*

*Thread 0: Number of terms:*

*4*

*Thread 1: Number of terms:*

*5*

*Thread 2: Number of terms:*

*8*

*[**New Thread 0x7ffff77fe700 (LWP 3325)]***

***[New Thread 0x7ffff6ffd700 (LWP 3326)]***

***[New Thread 0x7ffff67fc700 (LWP 3327)]***

*Breakpoint 1, main () at fibonacci_threads.c:49*

*49 for ( i = 0; i < NUM_THREADS; i++ )*

We can see from the output above that gdb is somehow aware of the extra three threads being created ( [New Thread 0x7fff... ]). Because we knew the program already we could safely assume that those threads are the three worker threads by the program. But how to check that those threads are indeed the threads that we think they are?

First command useful in this context is “**info threads**”. This command is used to inspect how many threads were created by the program by the time the breakpoint was hit:

*(gdb) info threads                                                                                                                                                 *

 *Id Target Id Frame*

 *4 Thread 0x7ffff67fc700 (LWP 3194) "fibonacci_threa" 0x00007ffff78f53a1 in clone () from /lib64/libc.so.6*

 *3 Thread 0x7ffff6ffd700 (LWP 3193) "fibonacci_threa" 0x00007ffff78bc8ad in nanosleep () from /lib64/libc.so.6*

 *2 Thread 0x7ffff77fe700 (LWP 3192) "fibonacci_threa" 0x00007ffff78bc8ad in nanosleep () from /lib64/libc.so.6*

** 1 Thread 0x7ffff7fdf740 (LWP 3188) "fibonacci_threa" main () at fibonacci_threads.c:49*

From the output of the “info threads” I can see that the fibonacci_thread contains four threads. This is the number of threads I expect to see being created at line 48\. One thread (id 1) is the main thread of the application. The other three threads (id 2,3 and 4) are the three worker threads created at line 44\. There is also a “*” marker for thread id 1\. This means that the thread id 1 has the focus. All gdb commands are executed against the thread that has the focus.

*(gdb) bt*

*#0 main () at fibonacci_threads.c:49*

*(gdb) info local*

*tid = {140737345742592, 140737337349888, 140737328957184}*

*n = {4, 5, 8}*

*i = 3*

Note that once a breakpoint is hit for a multithreaded program the execution of all the threads stops and not only for the thread that hit the breakpoint. This allows the examination of the overall state of the program, without the risk that things may change in other threads while one thread is stopped for inspection.

The “**t**” (“**thread**”) command allows changing the thread that has the focus so that the context of that thread can be inspected. Below is for example how to switch the focus to the thread with the id of 3.

*(gdb) t 3*

*[Switching to thread 3 (Thread 0x7ffff6ffd700 (LWP 3193))]*

*#0 0x00007ffff78bc8ad in nanosleep () from /lib64/libc.so.6*

*(gdb) bt*

*#0 0x00007ffff78bc8ad in nanosleep () from /lib64/libc.so.6*

*#1 0x00007ffff78bc744 in sleep () from /lib64/libc.so.6*

*#2 0x00000000004007fe in fibonacci (arg=0x5) at fibonacci_threads.c:22*

*#3 0x00007ffff7bc7df3 in start_thread () from /lib64/libpthread.so.0*

*#4 0x00007ffff78f53dd in clone () from /lib64/libc.so.6*

But what happens if I set a breakpoint to a line that will be executed only by a worker thread. Like line 11 from my example. Will this breakpoint be hit or not? Lets try this scenario:

*(gdb) b 11*

*Breakpoint 1 at 0x4007c1: file fibonacci_threads.c, line 11.*

*(gdb) r*

*Starting program: /home/ssosiade/books/linux_building/fibonacci_threads*

*[Thread debugging using libthread_db enabled]*

*Using host libthread_db library "/lib64/libthread_db.so.1".*

*Thread 0: Number of terms:*

*4*

*Thread 1: Number of terms:*

*5*

*Thread 2: Number of terms:*

*8*

*[New Thread 0x7ffff77fe700 (LWP 3339)]*

*[Switching to Thread 0x7ffff77fe700 (LWP 3339)]*

*Breakpoint 1, fibonacci (arg=0x4) at fibonacci_threads.c:12*

*12 for ( i = 0 ; i < n ; i++ )*

*(gdb) info threads*

*[New Thread 0x7ffff6ffd700 (LWP 3340)]*

 *Id Target Id Frame*

 *3 Thread 0x7ffff6ffd700 (LWP 3340) "fibonacci_threa" 0x00007ffff78f53a1 in clone () from /lib64/libc.so.6*

** 2 Thread 0x7ffff77fe700 (LWP 3339) "fibonacci_threa" fibonacci (arg=0x4) at fibonacci_threads.c:12*

 *1 Thread 0x7ffff7fdf740 (LWP 3335) "fibonacci_threa" 0x00007ffff78f53a1 in clone () from /lib64/libc.so.6*

The conclusions that we can draw from here are:

· the breakpoint is hit only by one thread

· the thread that first hits the breakpoint gets the focus

Even if line 11 is common across all the three worker threads, one of them will be hitting this breakpoint first. In my example thread 2 hits the breakpoint first, which is somehow expected as this was the first worker thread created by the program. However accurately predicting which thread is reaching that line first is difficult as this depends entirely on multiple other factors (kernel scheduling policy, total number of threads in the system, other thread priorities, etc...). 

If I continue the execution of the program from where the breakpoint was hit, I can see that the breakpoint will be hit second time by the second worker thread (thread id 3). And this thread also gets the focus:

*(gdb) c*

*Continuing.*

*[Switching to Thread 0x7ffff6ffd700 (LWP 3340)]*

*Breakpoint 1, fibonacci (arg=0x5) at fibonacci_threads.c:12*

*12         for ( i = 0 ; i < n ; i++ )*

*(gdb) info threads*

*[New Thread 0x7ffff67fc700 (LWP 3418)]*

 *Id Target Id Frame*

 *4 Thread 0x7ffff67fc700 (LWP 3418) "fibonacci_threa" 0x00007ffff78f53a1 in clone () from /lib64/libc.so.6*

** 3 Thread 0x7ffff6ffd700 (LWP 3340) "fibonacci_threa" fibonacci (arg=0x5) at fibonacci_threads.c:12*

 *2 Thread 0x7ffff77fe700 (LWP 3339) "fibonacci_threa" 0x00007ffff78bc8ad in nanosleep () from /lib64/libc.so.6*

 *1 Thread 0x7ffff7fdf740 (LWP 3335) "fibonacci_threa" 0x00007ffff78f53a1 in clone () from /lib64/libc.so.6*

These are in a nutshell the fundamentals of dealing with multithreaded Linux programs under gdb: detecting what threads are part of the program and switching the context among them in order to explore the internal state of each thread.

## Dealing with crashes

One of the most powerful feature of gdb is investigating what traditionally has been a difficult issue to deal with: program crashes. A crash that happens randomly without any apparent reason is notoriously difficult to investigate without having a way to get some context about what led to the program crash. And this is where gdb can assist with, to provide the backtrace to where the crash happened and give information about the context of each call frame leading to the crash.

Below is a program that was written in such a way that will deliberately crash during the execution.

*#include<stdio.h>*

*void functionC() {*

 *int *p = NULL;*

 **p = 25;*

*}*

*void functionB() {*

 *functionC();*

*}*

*void functionA() {*

 *functionB();*

*}*

*int main()*

*{*

 *printf("Program started\n");*

 *functionA();*

 *printf("Program finished\n");*

 *return 0;*

*}*

Assuming that the source code above is located in a file called “crashy.c” I can build this program with the following command:

*$ gcc -g crashy.c -o crashy*

Next I am going to pretend that I don’t know what is causing this program to crash and I will be using gdb to assist me in pinpointing the root cause for the crash.

To be able to investigate program crashes I need to instruct the operating system to save the crash data. I can do this by issuing the following command:

*$ ulimit -c unlimited*

The crash data is stored in a particular Linux file called: “core file”. A core file is essentially a snapshot of the system, including memory and CPU registers just at the point when the crash occurred. The command above will enable the core file of unlimited size. By default the core size is zero, meaning that no core file is produced. The core files can be also set to a particular maximum size but the risk here that the produced core file may not contain enough information to assist with the debugging. Therefore it is recommended that the core file size to be set to “unlimited” assuming there are no strict restrictions with regards to storage space.

Lets run the “crashy” program providing the core files generation is now enabled. This will produce the following output:

*$ ./crashy*

*Program started*

*Segmentation fault (core dumped)*

I can see in the output some indication that a core file was generated. And if I list the content of the folder then I can see that the core file has been generated indeed:

*$ ls -lrt*

*-rw-rw-r--. 1 ssosiade ssosiade 256 Feb 23 12:07 crashy.c*

*-rwxrwxr-x. 1 ssosiade ssosiade 9830 Feb 23 12:08 crashy*

*-rw-------. 1 ssosiade ssosiade 253952 Feb 23 12:20 core.4890*

*$ file core.4890*

*core.4890: ELF 64-bit LSB core file x86-64, version 1 (SYSV), SVR4-style, from './crashy'*

Note that by default the naming convention for the core file is core_<pid> where pid is process id of the process that caused the crash.

I can run the gdb against the crash file generated using the following command:

*$ gdb crashy core.4890*

*GNU gdb (GDB) Red Hat Enterprise Linux 7.6.1-80.el7*

*Copyright (C) 2013 Free Software Foundation, Inc.*

*License GPLv3+: GNU GPL version 3 or later <http://gnu.org/licenses/gpl.html>*

*This is free software: you are free to change and redistribute it.*

*There is NO WARRANTY, to the extent permitted by law. Type "show copying"*

*and "show warranty" for details.*

*This GDB was configured as "x86_64-redhat-linux-gnu".*

*For bug reporting instructions, please see:*

*<http://www.gnu.org/software/gdb/bugs/>...*

*Reading symbols from /home/ssosiade/book/crashy...done.*

*[New LWP 4890]*

*Core was generated by `./crashy'.*

*Program terminated with signal 11, Segmentation fault.*

***#0 0x0000000000400540 in functionC () at crashy.c:5***

***5 *p = 25;***

Just by loading the crash file into gdb I get a fist indication about what caused the crash: the attempt to deference a null pointer at line 5: *p=25\. I can further explore the calling sequence that led my program to execute that instruction by using “**bt**” (**backtrace**) gdb command:

*(gdb) bt*

*#0 0x0000000000400540 in functionC () at crashy.c:5*

*#1 0x0000000000400556 in functionB () at crashy.c:9*

*#2 0x0000000000400566 in functionA () at crashy.c:13*

*#3 0x0000000000400580 in main () at crashy.c:19*

I can continue investigating the context of the program and look at the state of the execution for all the threads, local and public variables, CPU registers, memory, files in use during execution or source files:

***(gdb) info local***

*p = 0x0*

***(gdb) info threads***

 *Id Target Id Frame*

** 1 LWP 4890 0x0000000000400540 in functionC () at crashy.c:5*

*(gdb) info registers*

*rax 0x0 0*

*rbx           0x0 0*

*rcx 0x7fcd73a97a30 140520385509936*

*rdx 0x7fcd73d6ca10 140520388479504*

*rsi 0x7fcd73f90000 140520390721536*

*rdi 0x1 1*

*rbp 0x7ffd0ed4a1c0      0x7ffd0ed4a1c0*

*rsp 0x7ffd0ed4a1c0 0x7ffd0ed4a1c0*

*r8 0xffffffff 4294967295*

*r9 0x0 0*

*r10 0x22 34*

*r11 0x246 582*

*r12     0x400440 4195392*

*r13 0x7ffd0ed4a2d0 140724852269776*

*r14 0x0 0*

*r15 0x0 0*

*rip 0x400540 0x400540 <functionC+16>*

*eflags 0x10246              [ PF ZF IF RF ]*

*cs 0x33 51*

*ss 0x2b 43*

*ds 0x0 0*

*es 0x0 0*

*fs 0x0 0*

*gs 0x0              0*

***(gdb) info files***

*Symbols from "/home/ssosiade/book/crashy".*

*Local core dump file:*

 *`/home/ssosiade/book/core.4890', file type elf64-x86-64.*

 *0x0000000000400000 - 0x0000000000401000 is load1*

 *0x0000000000600000 - 0x0000000000601000 is load2*

 *0x0000000000601000 - 0x0000000000602000 is load3*

 *0x00007fcd739b0000 - 0x00007fcd739b1000 is load4a*

*… <info omitted for brevity>*

 *0x00007fcd73f92b80 - 0x00007fcd73f92dec is .data.rel.ro in /lib64/ld-linux-x86-64.so.2*

 *0x00007fcd73f92df0 - 0x00007fcd73f92fa0 is .dynamic in /lib64/ld-linux-x86-64.so.2*

 *0x00007fcd73f92fa0 - 0x00007fcd73f92ff8 is .got in /lib64/ld-linux-x86-64.so.2*

 *0x00007fcd73f93000 - 0x00007fcd73f93ff8 is .data in /lib64/ld-linux-x86-64.so.2*

 *0x00007fcd73f94000 - 0x00007fcd73f94208 is .bss in /lib64/ld-linux-x86-64.so.2*

***(gdb) info sources***

*Source files for which symbols have been read in:*

*/home/ssosiade/book/crashy.c*

*Source files for which symbols will be read in on demand:*

***(gdb) info source***

*Current source file is crashy.c*

*Compilation directory is /home/ssosiade/book*

*Located in /home/ssosiade/book/crashy.c*

*Contains 22 lines.*

*Source language is c.*

*Compiled with DWARF 2 debugging format.*

*Does not include preprocessor macro info.*

All of the above are invaluable when trying to diagnose the root cause for a random crash. The gdb capability to decode core dumps and provide information about the context of a crash is a powerful feature. Just try to imagine how difficult investigating crashes could be without the crash information provided by gdb.

## Running gdb with text user interface

“TUI” stands for “Text User Interface” and represents a feature of gdb that allows debugging by using multiple windows in text mode. 

The following windows are available in TUI mode:

· ***Command*** *-* represents the gdb command window where gdb commands can be issued. This window is always visible.

· ***Source*** *-* shows the source file of the program.

· ***Assembly*** *-* shows the program assembly language.

· ***Register*** *-* displays the processor registers and their content.

To launch gdb in text user interface mode use the following command:

*$ gdb fibonacci –tui*

By default the command window and the source window are displayed, as shown in the picture below:

![](images/00010.jpeg)

The source and assembly windows show the program line being executed by using the ‘>’ marker.

If breakpoints are set then these are displayed for each line of the program by using the following naming convention: <*breakpoint_type*><b*reakpoint_status*>.

Where *<breakpoint_type>* can have one of the following representation and meaning:

B - breakpoint hit at least once.

B - breakpoint not hit so far.

H - hardware breakpoint hit at least once.

h - hardware breakpoint not hit so far.

The *<breakpoint_status>* indicates whether the breakpoint is enabled or not and has one of the following values:

+ breakpoint is enabled.

- breakpoint is disabled.

To see what windows are currently in use type the following command in the command window:

*(gdb) info win*

 *SRC (29 lines) <has focus>*

 *CMD (14 lines)*

To display a particular window use one of the following “**layout**” command:

*(gdb) layout asm*

*(gdb) layout src*

*(gdb) layout reg*

Among multiple windows that can displayed at a time, only one can have the focus. A windows that has the focus can be scrolled up and down. The “**focus**” command can be used in order to set the focus to a particular window:

*(gdb) focus src*

*Focus set to SRC window.*

*(gdb) focus reg*

*Focus set to REGS window.*

*(gdb) focus cmd*

*Focus set to CMD window.*

*(gdb) focus asm*

*Focus set to ASM window.*

And finally, use “**refresh**” command in order to refresh all the windows currently in use.

*(gdb) refresh*

During a debugging session several gdb commands can be issued in the command window. These commands can alter the internal state of the program without necessarily having all the internal changes reflected on windows enabled on the screen. Therefore I recommend using “refresh” command before making any decision based on the data present in the text mode windows.

# Debugging memory access problems. Valgrind

Although it is not part of the GNU toolchain, valgrind is probably the most common tool in Linux for detecting various memory related issues. For this reason I decided to dedicate a small chapter of this book on this tool.

Some Linux distributions usually include or allow the user to include this package when installing the operating system.

In order to check whether Valgrind is installed or not on your machine you can do:

*$ which valgrind*

*/usr/bin/valgrind*

If you do not have it then you can simply yum install it:

*$ sudo yum –y install valgrind*

Lets see this tool in action. I am going to present an example on how to use this tool in order to detect memory leaks. Here is a program that allocates some memory at line 8 but “forgets” to free it.

 *1: #include <stdio.h>*

* 2: #include <stdlib.h>*

* 3:*

* 4: #define BUFFER_SIZE 12*

* 5:*

* 6: int main() {*

* 7: char *buffer;*

* 8:*

* 9: buffer = malloc(BUFFER_SIZE);*

*10: if (buffer == NULL) {*

*11: printf("Failed to allocate memory\n");*

*12: return 1;*

*13: }*

*14:*

*15: printf("Memory allocated successfully\n");*

*16: return 0;*

*17: }*

The program compiles and runs successfully:

*$ gcc leaky.c -o leaky*

*$ ./leaky*

*Memory allocated successfully*

The following report will be produced when running this program against valgrind:

*$ valgrind ./leaky*

*==19945== Memcheck, a memory error detector*

*==19945== Copyright (C) 2002-2012, and GNU GPL'd, by Julian Seward et al.*

*==19945== Using Valgrind-3.8.1 and LibVEX; rerun with -h for copyright info*

*==19945== Command: ./leaky*

*==19945==*

*Memory allocated successfully*

*==19945==*

*==19945== HEAP SUMMARY:*

*==19945== in use at exit: 12 bytes in 1 blocks*

***==19945== total heap usage: 1 allocs, 0 frees, 12 bytes allocated***

*==19945==*

*==19945== LEAK SUMMARY:*

***==19945== definitely lost: 12 bytes in 1 blocks***

*==19945== indirectly lost: 0 bytes in 0 blocks*

*==19945== possibly lost: 0 bytes in 0 blocks*

*==19945== still reachable: 0 bytes in 0 blocks*

*==19945== suppressed: 0 bytes in 0 blocks*

*==19945== Rerun with --leak-check=full to see details of leaked memory*

*==19945==*

*==19945== For counts of detected and suppressed errors, rerun with: -v*

*==19945== ERROR SUMMARY: 0 errors from 0 contexts (suppressed: 6 from 6)*

The output says that there is a mismatch between the number of “allocs” and and “frees” and that I am leaking 12 bytes of heap memory – exactly how many bytes I dynamically allocated on line 9.

I can run valgrind with extra parameters in order to get more information about the origin of the problem:

*$ valgrind --tool=memcheck --leak-check=full ./leaky*

*==20039== Memcheck, a memory error detector*

*==20039== Copyright (C) 2002-2012, and GNU GPL'd, by Julian Seward et al.*

*==20039== Using Valgrind-3.8.1 and LibVEX; rerun with -h for copyright info*

*==20039== Command: ./leaky*

*==20039==*

*Memory allocated successfully*

*==20039==*

*==20039== HEAP SUMMARY:*

*==20039== in use at exit: 12 bytes in 1 blocks*

*==20039== total heap usage: 1 allocs, 0 frees, 12 bytes allocated*

*==20039==*

***==20039== 12 bytes in 1 blocks are definitely lost in loss record 1 of 1***

***==20039== at 0x4A06A2E: malloc (vg_replace_malloc.c:270)***

***==20039== by 0x400515: main (in /home/ssosiade/books/valgrind/leaky)***

*==20039==*

*==20039== LEAK SUMMARY:*

*==20039== definitely lost: 12 bytes in 1 blocks*

*==20039== indirectly lost: 0 bytes in 0 blocks*

*==20039== possibly lost: 0 bytes in 0 blocks*

*==20039== still reachable: 0 bytes in 0 blocks*

*==20039== suppressed: 0 bytes in 0 blocks*

*==20039==*

*==20039== For counts of detected and suppressed errors, rerun with: -v*

*==20039== ERROR SUMMARY: 1 errors from 1 contexts (suppressed: 6 from 6)*

As we can see in the output above the calling sequence that causes the leak is displayed so all I have to do is to trace back to the “malloc” that is the cause for the memory leak and add the corresponding “free” for it.

*==20039== 12 bytes in 1 blocks are definitely lost in loss record 1 of 1*

*==20039== at 0x4A06A2E: malloc (vg_replace_malloc.c:270)*

*==20039== by 0x400515: main (in /home/books/valgrind/leaky)*

I can fix this program now by adding a free just before the program finishes:

* 1: #include <stdio.h>*

* 2: #include <stdlib.h>*

* 3:*

* 4: #define BUFFER_SIZE 12*

* 5:*

* 6: int main() {*

* 7: char *buffer;*

* 8:*

* 9: buffer = malloc(BUFFER_SIZE);*

*10: if (buffer == NULL) {*

*11: printf("Failed to allocate memory\n");*

*12: return 1;*

*13: }*

*14:*

*15: printf("Memory allocated successfully\n");*

***16: free(buffer);***

*17: return 0;*

*18: }*

If I run the program again under valgrind tool I will see no errors this time:

*$ valgrind --tool=memcheck --leak-check=full ./leaky*

*==20156== Memcheck, a memory error detector*

*==20156== Copyright (C) 2002-2012, and GNU GPL'd, by Julian Seward et al.*

*==20156== Using Valgrind-3.8.1 and LibVEX; rerun with -h for copyright info*

*==20156== Command: ./leaky*

*==20156==*

*Memory allocated succesfuly*

*==20156==*

*==20156== HEAP SUMMARY:*

*==20156== in use at exit: 0 bytes in 0 blocks*

*==20156== total heap usage: 1 allocs, 1 frees, 12 bytes allocated*

*==20156==*

*==20156== All heap blocks were freed -- no leaks are possible*

*==20156==*

*==20156== For counts of detected and suppressed errors, rerun with: -v*

***==20156== ERROR SUMMARY: 0 errors from 0 contexts (suppressed: 6 from 6)***

Memory leaks are not the only types of problems that valgrind can detect. This tool is very powerful in detecting the following other memory access related issues:

· Accessing memory that is not part of the program (for example overrunning heap blocks, writing memory beyond the top of the stack or accessing memory after it has been freed).

· Using values that have not been initialized.

· Multiple freeing of dynamic memory or mismatch in useing of malloc vs. free or new vs. Delete.

· Overlapped “source” and “destination” pointers use in functions for string or memory manipulation.