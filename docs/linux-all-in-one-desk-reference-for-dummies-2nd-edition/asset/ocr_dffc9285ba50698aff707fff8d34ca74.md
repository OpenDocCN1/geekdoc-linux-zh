Table 1-1 (continued)  
| Option | Meaning |
| -mcpu=cputype | Optimize code for a specific processor. cputype can take many different values—some common ones are i386, i486, i586, i686, pentium, pentiumpro, pentium2, pentium3, pentium4. |
| -o FILE | Generate the specified output file (used to designate the name of an executable file) |
| -00 (two zeros) | Do not optimize |
| -0 or -01 (letter 0) | Optimize the generated code |
| -02 (letter 0) | Optimize even more |
| -03 (letter 0) | Perform optimizations beyond those done for -02 |
| -Os (letter 0) | Optimize for size (to reduce the total amount of code) |
| -pedantic | Generate errors if any non-ANSI standard extensions are used |
| -pg | Add extra code to the program so that, when run, it generates information the gprof program can use to display timing details for various parts of the program |
| -shared | Generate a shared object file (typically used to create a shared library) |
| -UNACRO | Undefine the specified macro |
| -v | Display the version number of GCC |
| -w | Don't generate any warning messages |
| -W1, OPTION | Pass the OPTION string (containing multiple comma-separated opts) to the linker. To create a shared library named libXXX.so.1, for example, use the following flag: -W1,-soname,libXXX.so.1. |

# # The GNU make utility

When an application is made up of more than a few source files, compiling and linking the files by manually typing the gcc command can get very tiresome. Also, you don't want to compile every file whenever you change something in a single source file. These situations are where the GNU make utility comes to your rescue.

The make utility works by reading and interpreting a makefile—a text file that describes which files are required to build a particular program, as well as how to compile and link the files to build the program. Whenever you change one or more files, make determines which files to recompile—and it issues the appropriate commands for compiling those files and rebuilding the program.