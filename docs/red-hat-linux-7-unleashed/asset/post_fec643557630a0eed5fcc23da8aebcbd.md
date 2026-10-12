
# New Features of the GNU egcs Compiler System

The *egcs* (pronounced “eggs”) program suite originally was an experimental version of the *gcc* compiler whose development was first hosted by Cygnus Support (which is now part of Red Hat). Starting with Red Hat 5.1 for Intel, *egcs* was made available for installation as part of your Red Hat Linux system.

When first being developed, Cygnus described *egcs* as an experimental step in the development of *gcc*. Since its first release in late summer 1997, *egcs* has incorporated many of the latest developments and features from *parallel* development of *gcc* with many new developments of its own, such as a built-in Fortran 77, Java, and Objective C front ends. Some people have suggested that the name be changed from “Experimental GNU Compiler System” to “Enhanced GNU Compiler System.”

> You will need to use the *gcj* front end to the *egcs* compiler to compile Java language classes. The front-end software and related packages should be included with Red Hat Linux, but you can find out more about *egcs* Java support by browsing to *http://sources.redhat.com/java/compiler.html* Intrepid Linux developers can jump right to the source code tree for the latest *egcs* and Java support software via the Red Hat Web site.

Although some Linux developers may have felt that development of *egcs* represented a fork (or split) in *gcc* compiler development, Cygnus stated that cooperation between the developers of *gcc* and *egcs* would prevent this. The hope, according to Cygnus, was that the new compiler architecture and features of *egcs* would help *gcc* be the best compiler in the world.

In April 1999, *egcs* officially became part of future GNU *gcc* software, and according to Cygnus, the *egcs* team will be responsible for rolling out future GCC releases. We can only hope that Red Hat will live up to that commitment.

Problems might occur when you are using *egcs* if you try to build a software package written in C++ that references *gcc* in its Makefile.

## Linux C/C++ Programming Tools

![](img/6bd28cbdb5cafd4e9d424d0c660b83ee_816_0.png)

The Makefile script may contain names and locations of programs and files used during the build process. The wxw Makefile contained the following two definitions:

```
CC     = gcc
CXX    = gcc
```

While this will work if you have only gcc installed, if you install the egcs suite, you will need to change the name of the designated C++ compiler in your Makefile to g++, like this:

```
CC     = gcc
CXX    = g++
```

Just be aware that if you use egcs to compile C++ source files (files ending in .c, .cc, or .cxx), you might have to fix the software’s Makefile first.

For more information about egcs and the latest updates, versions, or feature news about egcs, browse to http://www.gnu.org/software/gcc/gcc.html. You will find an egcs FAQ and pointers to the latest stable egcs release, or snapshots of the most recent development version.

## Additional Resources

If you are interested in learning more about C and C++, you should look for the following books:

- *Sams Teach Yourself C in 21 Days*, by Peter Aitken and Bradley Jones, Sams Publishing.
- *Sams Teach Yourself C++ for Linux in 21 Days*, by Jesse Liberty and David B. Horvath, CCP, Sams Publishing.
- *C How to Program and C++ How to Program*, by H. M. Deitel and P. J. Deitel.
- *The C Programming Language*, by Brian Kernighan and Dennis Ritchie.
- *The Annotated C++ Reference Manual*, by Margaret Ellis and Bjarne Stroustrup.
- *Programming in ANSI C*, by Stephen G. Kochan.

## Summary

UNIX was built on the C language. C is a platform-independent, compiled, procedural language based on functions and the capability to derive new, programmer-defined data structures.

C++ extends the capabilities of C by providing the necessary features for object-oriented design and code. C++ compilers such as **gcc** correctly compile ANSI C code. C++ also provides some features, such as the capability to associate functions with data structures, that do not require the use of full, class-based, object-oriented techniques. For these reasons, the C++ language allows existing UNIX programs to migrate toward the adoption of object orientation over time.

Red Hat Linux is full of tools that make your life as a C/C++ programmer easier. There are tools to create your program (editors), compile it (**gcc** and **egcs**), create libraries (**ar**), control the source (RCS and CVS), build your code (**make**), debug it (**gdb** and **xgdb**), and finally, determine where inefficiencies lie (**gprof**). Take advantage of the environment!

![](img/6bd28cbdb5cafd4e9d424d0c660b83ee_820_0.png)
![](img/6bd28cbdb5cafd4e9d424d0c660b83ee_820_1.png)

# Shell Scripting

## In This Chapter

- Creating and Executing a Shell Program 785
- Variables 788
- Positional Parameters 789
- Built-In Variables 790
- Special Characters 791
- Comparison of Expressions 794
- Iteration Statements 802
- Conditional Statements 807
- Miscellaneous Statements 811
- Functions 811

When you enter commands from the command line, you are entering commands one at a time and getting a response from the system. From time to time, you will need to execute more than one command, one after the other, and get the final result. You can do so with a *shell program* or *shell script*. A shell program is a series of Linux commands and utilities that have been put into a file by using a text editor. When you execute a shell program, the commands are interpreted and executed by Linux one after the other.

You can write shell programs and execute them like any other command under Linux. You can also execute other shell programs from within a shell program if they are in the search path. A shell program is like any other programming language and has its own syntax. You can define variables, assign various values, and so on. These functions are discussed in this chapter.

The Red Hat Linux CD-ROMs that accompany this book come with a rich assortment of capable, flexible, and powerful shells. These shells have numerous built-in commands, configurable command-line prompts, and features such as command-line history and editing. Table 25.1 lists each shell, along with its description and location in your Red Hat Linux filesystem.

**TABLE 25.1 Shells with Red Hat Linux**

| Name | Description | Location |
|---|---|---|
| ash | A small shell (sh-like) | /bin/ash |
| ash.static | A version of ash not dependent on software libraries | /bin/ash.static |
| bash | The Bourne Again Shell | /bin/bash |
| bsh | A symbolic link to ash | /bin/bsh |
| csh | The C shell, a symbolic link to tesh | /bin/csh |
| ksh | The public-domain Korn shell | /bin/ksh, /usr/bin/ksh |
| pdksh | A symbolic link to ksh | /usr/bin/pdksh |
| rsh | The restricted shell (for network operation) | /usr/bin/rsh |
| sh | A symbolic link to bash | /bin/sh |
| tesh | A csh-compatible shell | /bin/tesh |
| zsh | A compatible csh, ksh, and sh shell | /bin/zsh |

## Creating and Executing a Shell Program

Say you want to set up a number of aliases whenever you log on. Instead of typing all of the aliases every time you log on, you can put them in a file by using a text editor, such as vi, and then execute the file.

Here is what is contained in myenv, a sample file created for this purpose (for bash):

```
#!/bin/sh
alias 11='ls -1'
alias dir='ls'
alias copy='cp'
```

myenv can be executed in a variety of ways under Linux.

You can make myenv executable by using the chmod command, as follows, and then execute it as you would any other native Linux command:

```
# chmod +x myenv
```

This turns on the executable permission of myenv. You need to ensure one more thing before you can execute myenv—it must be in the search path. You can get the search path by executing

```
# echo $PATH
```

If the directory where the file myenv is located is not in the current search path, you must add the directory name in the search path.

Now you can execute the file myenv from the command line as if it were a Linux command:

```
# myenv
```

### Note
The first line in your shell program should start with a pound sign (#), which tells the shell that the line is a comment. Following the pound sign, you must have an exclamation point (!), which tells the shell to run the command following the exclamation point and to use the rest of the file as input for that command. This is common practice for all shell scripting. For example, if you wrote a shell script for bash, the first line of your script will contain #!/bin/bash.
