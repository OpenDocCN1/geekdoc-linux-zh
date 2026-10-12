# Variables (or macros)

In addition to the basic capability of building targets from dependents, GNU make includes many nice features that make it easy for you to express the dependencies and rules for building a target from its dependents. If you need to compile a large number of C++ files by using GCC with the same options, for example, typing the options for each file is tedious. You can avoid this repetitive task by defining a variable or macro in make as follows:

```
```make
# Define macros for name of compiler
CXX= g++
# Define a macro for the GCC flags
CXXFLAGS= -O2 -g -mcpu=i686
# A rule for building an object file
form.o: form.c form.h
    $(CXX) -c $(CXXFLAGS) form.c
```
```

In this example, CXX and CXXFLAGS are make variables. (GNU make prefers to call them variables, but most UNIX make utilities call them macros.)

To use a variable anywhere in the makefile, start with a dollar sign ($) followed by the variable within parentheses. GNU make replaces all occurrences of a variable with its definition; thus it replaces all occurrences of $(CXXFLAGS) with the string -O2 -g -mcpu=i686.

GNU make has several predefined variables that have special meanings. Table 1-2 lists these variables. In addition to the variables listed in Table 1-2, GNU make considers all environment variables (such as PATH and HOME) to be predefined variables as well.

**Table 1-2 Some Predefined Variables in GNU make**

| Variable | Meaning |
|---|---|
| $% | Member name for targets that are archives. If the target is libDisp.a(image.o), for example, $% is image.o, and $@ is libDisp.a. |
| $* | Name of the target file without the extension. |
| $+ | Names of all dependent files with duplicate dependencies, listed in their order of occurrence. |
| $< | The name of the first dependent file. |
| $? | Names of all dependent files (with spaces between the names) that are newer than the target. |
| $@ | Complete name of the target. |