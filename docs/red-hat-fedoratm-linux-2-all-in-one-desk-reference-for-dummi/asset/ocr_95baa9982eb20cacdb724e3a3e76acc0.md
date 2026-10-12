# Table 1-2 (continued)

| Variable | Meaning |
| :--- | :--- |
| $^ | Names of all dependent files, with spaces between the names. Duplicates are removed from the dependent filenames. |
| AR | Name of the archive-maintaining program (Default value: ar). |
| ARFLAGS | Flags for the archive-maintaining program (Default value: rv). |
| AS | Name of the assembler program that converts the assembly language to object code (Default value: as). |
| ASFLAGS | Flags for the assembler. |
| CC | Name of the C compiler (Default value: cc). |
| CFLAGS | Flags that are passed to the C compiler. |
| CO | Name of the program that extracts a file from RCS (Default value: co). |
| COFLAGS | Flags for the RCS co program. |
| CPP | Name of the C preprocessor (Default value: ${CC} -E). |
| CPPFLAGS | Flags for the C preprocessor. |
| CXX | Name of the C++ compiler (Default value: g++). |
| CXXFLAGS | Flags that are passed to the C++ compiler. |
| FC | Name of the FORTRAN compiler (Default value: f77). |
| FFLAGS | Flags for the FORTRAN compiler. |
| LDFLAGS | Flags for the compiler when it is supposed to invoke the linker ld. |
| RM | Name of the command to delete a file (Default value: rm -f). |

# *A sample makefile*

You can write a makefile easily if you use the predefined variables of GNU *make* and its built-in rules. Consider, for example, a makefile that creates the executable *xdraw* from three C source files (*xdraw.c*, *xviewobj.c*, and *shapes.c*) and two header files (*xdraw.h* and *shapes.h*). Assume that each source file includes one of the header files. Given these facts, here is what a sample makefile may look like:

```
```
############################################
# Sample makefile
# Comments start with '#'
############################################

# Use standard variables to define compile and link flags

CFLAGS= -g -O2
# Define the target "all"
```
```