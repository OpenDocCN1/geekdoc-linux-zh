
# CHAPTER 21 Introduction to C/C++ Programming Tools

If you perform a full installation of Red Hat Linux from this book's CD-ROMs, you'll also be able to write Fortran 77, Java, 8086 assembler, and 80386 assembler language programs. This chapter focuses on C- and C++-related tools for Linux, such as the GNU C compiler (gcc) system, and prototyping environments for GNOME and the K Desktop Environment (KDE). The information presented here introduces some of the commands used to compile C and C++ programs, along with information about related programming tools.

# Programming in C with Linux

C is the programming language that is most frequently associated with UNIX. Since the 1970s, the bulk of the UNIX operating system and its applications have been written in C. Because the C language doesn't directly rely on any specific hardware architecture, UNIX was one of the first portable operating systems. In other words, the majority of the code that makes up UNIX doesn't know and doesn't care which computer it is actually running. Machine-specific features are isolated in a few modules within the UNIX kernel, which makes it easy for you to modify when you are porting to different hardware architectures.

> In 1983, the American National Standards Institute (ANSI) established a committee to standardize the definition of C. The resulting standard is known as ANSI C, and it is the recognized standard for the language, the grammar, and a core set of libraries. The syntax is slightly different from that of the original C language, which is frequently called K&R, for Kernigan and Ritchie. There is also an International Standards Organization (ISO) C that is very similar to the ANSI standard.

C is a programming language you can use to create programs for Linux. The C language is used in text files source code. The source code are read by programs included with the GNU gcc suite during the process of building a new Linux program. C is a compiled language, which means that C code is first analyzed by the preprocessor and translated into assembly language and then into machine instructions that are appropriate to the target CPU. An assembler creates a binary, or object, file from the machine instructions. The final object is linked to any required external software support by the linker. A C program is stored in a text file that ends with a .c extension and always contains at least one routine, or function, such as main(). Functions are the commands that perform each step of the task that the C program was written to accomplish.

The Linux kernel is mostly written in C, a programming language that can be used to create programs that build and run on many different platforms. This portability is one of the reasons Linux works with so many different processing units (CPUs). To learn more about building the Linux kernel from source using installed Linux software development tools, see Chapter 24, "Kernel and Module Management."

# Programming in C++

C++ is an object-oriented extension to C. Because C++ is a superset of C, C++ compilers compile C programs correctly, and it is possible to write non-object-oriented code in C++.

The distinction between an object-oriented language as C++ and a procedural one as C can be subtle and hard to grasp, especially with regard to C++, which retains all of C's characteristics and concepts. One way to describe the difference is to say that when programmers code in C, they specify actions that process the data; when they write code in C++, they create data objects that can be requested to perform actions on or with regard to themselves.

Thus, a function receives one or more values as input, transforms or acts on them in some way, and returns a result. If the values passed include pointers, the contents of data variables can be modified by the function. It is likely that the code that is calling a function does not know, and does not to know, what steps the function takes when it is invoked.

Functions, the procedures that take place in a computer program, are associated with C++ objects as well. But the actions performed when an object's function is invoked can operate differently, perhaps substantially, depending on the specific type of the data structure with which it is associated. This is known as overloading function names. Overloading relates to a second characteristic of C++: the fact that functions can be defined as belonging to C++ data structures, and of the wider language feature known as encapsulation.

In addition to overloading and encapsulation, object-oriented languages allow programmers to define new abstract types (including associated functions) and then derive subsequent data types from them. The notion of a new class of data objects, in addition to the built-in classes such as integer, floating-point number, and character, goes beyond the familiar capability to define complex data objects in C.

C++ extends the capabilities of C by providing the necessary features for object-oriented design and code. C++ compilers such as gcc correctly compile ANSI C code. C++ also provides some features, such as the capability to associate functions with data structures, that do not require the use of full, class-based, object-oriented techniques. For these reasons, the C++ language allows existing UNIX programs to migrate toward the adoption of object orientation over time.

Support for C++ programming using Red Hat Linux is provided by gcc, which you run with the name g++ when you're compiling C++ code. KDE includes some intermediate C++ tools, such as moc (the Meta Object Compiler) for use when building KDE applications.

> NOTE
You can read the C++ Programming HOWTO, available at http://www.tldp.org, for more information on programming using C++ and Linux.

# Getting Started with Linux/C++ Programming

Linux is C and C++ programmers because of gcc and its suite of related software-development tools, as gdb, autoconf, and make. Complex C programs may have dozens or hundreds of separate object files that are created during the process. One, more, or all these (compiled) steps may be carried out automatically by the gcc compiler, which is run by the make utility according to makefile. After a program is compiled, it can be executed over and over without recompilation.

Writing C programs for Linux requires you to understand C syntax, have some understanding of how to interface with the Linux kernel (using one or more different functions, known as system calls), and how to use programming tools such as gcc and make. You'll learn about each of these concepts and processes in this chapter.

To get started, you must make sure you have installed all the necessary software development packages (perhaps using the redhat-config-packages; see Chapter 8, "Managing Software and System Resources") to support your project. Installation of basic development software requires around 90MB of hard drive space. If you plan to build programs for the Linux kernel, you need the Kernel development packages and an additional 134MB of storage space.

Developing programs for the X Window System requires installation of about 40MB of software libraries, programming support files, and documentation. If you want to build GNOME clients, you need more than 60MB of additional space. If you intend to develop programs for KDE, you should plan on reserving 220MB or so of your hard drive to store KDE development software. Don't forget that you need lots of space for temporary files when you're building programs, as many intermediate files will be created during your programming sessions.

You should also become familiar with a good text editor. Although GNUists use the emacs environment to write, edit, and compile programs, many other developers do just fine with an editor as vi or pico for editing then use the command line to run tools.

When programming for GNOME or KDE, you might find it most convenient to use a graphical development project manager, such as GNOME's Glade (the GTK+ User Interface Builder) or KDE's Kdevel (the KDE development environment). These clients allow you to prototype an application with graphical tools, which frees you to concentrate on your client's interface. You can use either to automatically generate all necessary project and source code files for skeletal applications.
