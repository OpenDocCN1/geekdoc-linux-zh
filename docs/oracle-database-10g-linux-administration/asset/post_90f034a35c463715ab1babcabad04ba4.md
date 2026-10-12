
during boot, thus they will be available before /usr is mounted. Some of the utilities in /bin include the Linux shell programs, as listed next.

| Shell | Description |
| --- | --- |
| bash | The GNU Bourne-Again shell. This is the newest shell, incorporating features of both sh and ksh. Bash is the default shell program. |
| csh | csh was the first shell program that provided the ability to create shell programs resembling their C language cousins. It therefore allowed shell programmers to create sophisticated shell programs. |
| ksh | The Korn shell is a more sophisticated version of the basic Bourne shell. You can create complicated shell programs using ksh. |
| sh | sh is the original Bourne shell. This shell provides basic shell functionality as well as basic shell programming abilities. |
| tcsh | The tcsh is an enhanced csh that allows for command-line editing and completion. |
| zsh | zsh is a new shell that provides many of the features of ksh but has been enhanced to include spell checking, history, and so on. |

As you have heard before, Linux and UNIX are all about choices. You are free to use whichever shell you prefer.

## Utilities in /usr/bin

The utilities in /usr/bin are the utilities most likely to be used by the end user. These utilities are used for browsing directories, editing files, sending e-mail, and performing other tasks. The /usr/bin directory contains almost 1500 utilities that can be used by both the administrator and end user. These utilities also include many of the development environment utilities mentioned in the next section. A sample of some of the files in /usr/bin are shown next.

| Utility | Function |
| --- | --- |
| at | Used to run programs at a time in the future |
| awk | A pattern scanning and processing language |
| compress | Used to compress and expand files |
| cut | Prints selected parts of a file |
| diff | Compares files and prints differences |
| df | Displays available disk space |
| ftp | File Transport Protocol tool |
| ghostscript | Postscript and PDF interpreter |
| gzip | Used to compress and decompress files |
| less | Used to view the contents of files |
| lpr | Lineprinter interface; used to print files |
| mysql | The optional mysql database |
| perl | A sophisticated programming language interpreter |
| rsh | The remote shell processor |
| ssh | The secure shell processor |
| sudo | Used to run a program as root |
| tail | Reads from the end of a file |
| top | Displays top CPU processes |
| who | Displays a list of users on the system |
| zip | Used to compress and uncompress files |

I have not covered all of the utilities in detail because there are so many of them. As you become more familiar with Linux, you will become comfortable with a subset of these utilities that suit your needs and experience. You will find that you can use different utilities and applications to perform the same tasks with different levels of complexity and functionality. For example, you can write shell programs with any of the shells mentioned in the previous section, but you can also create sophisticated scripted programs using PERL. PERL is a sophisticated language that can easily call other applications, such as SQL*Plus.

## The Development Environment

The Linux development environment is quite sophisticated and full featured. It's mostly made up of the GNU compilers and libraries, as well as a wealth of system routines and libraries. The development environment supports C++, C, and assembly language programs, and thus it's heavily focused on C++ and C. Because Linux source code is written in C and is readily available for developers to modify and recompile, it is crucial that a robust C development environment be available within the Linux operating system.

The Linux development environment consists of the GNU compiler collection, the debugging tools, and the associated utilities, including

- The GNU compiler collection (gcc)
- cpp, the C preprocessor
- as, the assembler
- ld, the linker
- The GNU Debugger (gdb)
- The binutils, a set of binary utilities used by developers:
- ar, the archiver—creates, modifies and extracts files from code archives
- nm—used to list symbols within object files
- objcopy—used to copy and convert object files
- objdump—used to display the contents of a binary file
- ranlib—generates index to archive contents
- size—lists section and total sizes of object files
- strings—lists printable strings within files
- strip—discards symbols from files
- readelf—displays information about ELF format files

The development environment is very important to the Linux system, just as it is to UNIX systems. Linux is a dynamically configurable system which does not require the kernel to be relinked; however, Oracle does require a relink as part of its installation and configuration. It is necessary for the linker to be installed in order for Oracle to be installed.

The development environment available within Linux is similar to that offered on many UNIX platforms. In fact, the GNU compiler collection is available on many UNIX platforms. However, this development environment is very different from the development environment you would find under Windows. It is also unlike the graphical development environment you would get from Oracle, such as with JDeveloper.

Let’s look at some of the components of the Linux development environment.

## GCC, the GNU Compiler Collection

The GNU compiler collection consists of the C preprocessor, the assembler, and the linker. These components are all needed in order to process programs. Although the GNU compiler collection is typically invoked by using the command **gcc**, the individual components can be called separately.

You might wonder about the difference between C programs and C++ programs. The GNU compiler collection contains only one compiler, but will compile both C and C++ programs. The GNU compiler collection also compiles Objective C programs as well. The **gcc** command contains optimizations for different processors and systems and is considered one of the best performing compilers available today. In fact, many benchmarks use the GNU compiler collection.

**cpp**, the GNU preprocessor, performs functions such as macro expansion, conditional compiler directives, inclusion of header files, and line control. The preprocessor is the first step in creating binary executables from source code.
**as**, the GNU assembler, is used to create object files from assembly code files. The object files it creates are appended the .o suffix and are binary object files. Once you have created object files from C source files, they must be linked together with system object files.

**ld**, the GNU linker takes object files and links them together with system libraries and object files in order to create binary executable files or programs. Since the linker takes object files and combines them together to make executable files, it is not always necessary to have source code to all of your programs. Oracle ships with a set of object files that are taken and linked with system libraries and object files in order to create the Oracle executable. You don’t have access to Oracle source code, but at times you might need to create assembly language programs to replace some of Oracle’s functions. For example, in order to change the base address where Oracle runs, it is necessary to create an assembly language file called ksms.s and relink the Oracle binary. This is all done without having access to Oracle source code.

### The GNU Debugger

The GNU debugger allows you to create programs with special debug information included. This allows you to set breakpoints within the code and step through the code as it is executing. This is valuable in that it allows you to examine the contents of variables while the program is running. This might help you to determine where the problem is in the program itself—for instance, where a variable is being overloaded or where memory is not properly being released.

In addition, the debugger allows you to examine a program after it has terminated. The debugger may be able to help you determine where the program has terminated so you can fix it. For those of you who have done any type of system development, you will appreciate the debugger utility.

### The Binutils

The binutils are a collection of utilities used by developers to assist with the development, deployment, and debugging of Linux applications. They are simply a set of various GNU utilities that are packaged together, and consist of the following applications:

- **ar, the archiver** Creates, modifies, and extracts files from code archives. Code archives are libraries of object files used to organize these object files. Although an archive can be made up of any type of file, we are most likely concerned with object libraries. The ar utility is used to maintain object files within these libraries.
- **nm** Used to list symbols within object files. This is a very useful debug tool that can help you find symbols within object files.
