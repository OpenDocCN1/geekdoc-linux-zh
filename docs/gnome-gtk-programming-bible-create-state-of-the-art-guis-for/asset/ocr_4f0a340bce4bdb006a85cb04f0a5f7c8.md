software that results from compiling all of source in all of the subdirectories. There are two test statements that serve no purpose other than verifying that the script is being run in the current directory, and that the current directory contains the right things. In particular, the presence of a file named IDGBBIBLE and a directory named helloauto is assumed to indicate that the script is in the right place.

Your autogen.sh finishes by executing the autogen.sh in the macros subdirectory. There is a lot of output from this process. Text is output to both stdout and stderr. I suggest you look at this output so you can get an idea of what is going on; but because there is so much text generated, you need to capture it for later by using this:

```
autogen.sh <fred 2>&1
```

If all goes well (at least, if the script believes all went well) the last line printed is, "Enter 'make' to compile Hello Auto."

# The Main Makefile.am File

You need to create a file named Makefile.am in the main development directory. This file is used by autoconf to create Makefile.in. The Makefile.in file contains the description of a complete make file. The generated Makefile.in contains the information necessary to compile and link the entire system from scratch. It also contains special sets of instructions that undo the act of compiling and linking (make clean), install the previously compiled software (make install), and create a distribution package (make dist). Also, the autoconf program scans the source and determines all of the dependencies required for the final make file (such as which header files are included by which other source files).

The exact content of the Makefile.am file depends on how many subdirectories there are to include. In the following example, there is one source subdirectory (named helloauto) and the macros subdirectory containing a local copy of the macros:

```
SUBDIRS=macros helloauto
EXTRA_DIST=IDGBBIBLE
```

The Makefile.am file is composed of a list of macro definitions that act as input to automake. The top-level Makefile.am normally is quite simple as compared to those that reside in the directories with the source files. The name SUBDIRS is a space-separated list of all of the subdirectory names that contain other Makefile.am files. And those Makefile.am files can contain the names of other subdirectories containing Makefile.am files. While it is possible to specify a directory more than one level down, it is easier to maintain a system that has one Makefile.am file in each directory. The name EXTRA_DIST is defined as a space-separated list of files in the current directory that are to be included, along with the binary files, as part of the distribution of the software.