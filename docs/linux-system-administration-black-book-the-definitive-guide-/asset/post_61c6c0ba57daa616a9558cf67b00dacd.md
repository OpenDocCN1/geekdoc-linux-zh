
## Table 22.1 Commonly used preprocessor options available for gcc

| Option | Purpose | Value | Example |
| :--- | :--- | :--- | :--- |
| **-D** | Depending on usage, defines a macro that has a result of the string or defines a macro with a specific result **1** | Macro name or macro name and result | **-Done** or **-Dtwo='2'** |
| **-dD** | Outputs all macro definitions in their proper places | None | **-dD** |
| **-dN** | Outputs all macros as their **#define** statements | None | **-dN** |
| **-E** | Does the code preprocessing and then stops; see Table 22.2 for additional options for use with this option | None | **-E** |
| **-H** | Prints header file names | None | **-H** |
| **-idirafter** | Specifies the directory in which to look for header files if they are not found where they are expected | Path to look in | **-idirafter ~/ccode/headers** |
| **-imacros** | Processes the specified file before preprocessing the code, but discards its output | Path to file | **-imacros addthis** |
| **-include** | Processes the specified file before preprocessing the code | Path to file | **-include additions** |
| **-iprefix** | Specifies the prefix argument for the **-iwithprefix** option | Top directory | **-iprefix ~** |
| **-isystem** | Specifies an additional system header directory | Path | **-isystem ~/bin/sys** |
| **-iwithprefix** | Specifies a directory in which to look for header files if they are not found where they are expected, where this directory's path hangs off of the specified **-iprefix** directory | Remaining path | **-iwithprefix ccode/headers** |
| **-iwithprefixbefore** | Specifies a directory in which to look for header files initially, where this directory's path hangs off of the specified **-iprefix** directory | Remaining path | **-iwithprefixbefore ccode/headers** |
| **-MD** | Outputs statements that can be used for building a Makefile for this program, but saves the dependency information to a file with a .d extension so as to not interfere with the remaining compilation steps | None | **-MD** |
| **-MMD** | Outputs statements that can be used for building a Makefile for this program, but saves the dependency information to a file with a .d extension so as to not interfere with the remaining compilation steps; ignores system header files | None | **-MMD** |
| **-nostdinc** | Ignores system header directories | None | **-nostdinc** |
| **-trigraphs** | Ensures that standard C code is outputted, though this is often undesirable because of its strict nature | None | **-trigraphs** |
| **-U** | Undefines the specified macro | Macro name | **-Uthree** |
| **-undef** | Specifies that no macros should be defined unless specifically done so in the code | None | **-undef** |
| **-Wp,** | Passes a specific option— or more than one—to the preprocessor | Option(s), comma-separated if more than one | **-Wp,-MG** |

## Table 22.2 Options for use when only preprocessing with gcc

| Option | Purpose |
| :--- | :--- |
| **-C** | Leaves comments intact |
| **-dM** | Outputs only the macro definitions that have been set when preprocessing is finished |
| **-M** | Outputs statements that can be used for building a Makefile for this program |
| **-MG** | Outputs statements that can be used for building a Makefile for this program, assuming that the header files are in the same location as the source files |
| **-MM** | Outputs statements that can be used for building a Makefile for this program, but leaves out #include commands |
| **-P** | Leaves #line commands intact rather than expanding them |

5. After the preprocessor finishes, the compilation itself begins. Many options are available for compiling C code. Anyone who is used to compiling C programs knows that you sometimes end up with a lot of warning messages, some of which are meant to be ignored, whereas others are important. See Table 22.3 to choose from the warning options available to you. For this example, it is useful to make sure that items are defined before they are used. You now should have the following:

```
gcc -idirafter ~/bin/ccode/headers -MD -Wimplicit
```

> NOTE: The option -Wall activates many of the warnings listed in Table 22.3.

## Table 22.3 Commonly used warning options available for gcc during the compilation phase

| Option | Purpose |
| :--- | :--- |
| **-fsyntax-only** | Ignores everything but syntax errors |
| **-pedantic** | Gives warnings for everything that is not standard C; often not desirable, because standard C is very strict |
| **-pedantic-errors** | Produces error messages rather than warnings for anything that is not standard C |
| **-w** | Shuts off all warnings |
| **-Wchar-subscripts** | Produces a warning when an array subscript is assigned to the char type |
| **-Wcomment** | Warns regarding nested comments—two /* items without closing the comment—or if // appears in a comment |
| **-Werror** | Changes all warnings to error messages; not typically recommended if you use a lot of warnings |
| **-Werror-implicit-function-declaration** | Gives an error when a function is used before it is defined |
| **-Wformat** | Ensures that commands that require formatting arguments are being used properly |
| **-Wimplicit** | Uses both the -Wimplicit-int and -Wimplicit-function-declaration options |
| **-Wimplicit-function-declaration** | Warns when a function is used before it is defined |
| **-Wimplicit-int** | Warns when a variable declaration does not include a type declaration |
| **-Wmain** | Gives a warning if the main function has been given a bad type |
| **-Wmultichar** | Warns if any multicharacter constants were assigned |
| **-Wno-import** | Shuts off all warnings dealing with **import** statements |
| **-Wparentheses** | Warns about potential parentheses omissions |
| **-Wunuseed** | Combines several options that warn about variables, functions, and more that are created but not used anywhere in the code |

6. Several useful debugging switches also are available. See Table 22.4 for a list of the debugging switches that are available, and choose those that are appropriate. The important issue here is to make sure your code is **gprof**-readable. So, you now have the following:

```
gcc -idirafter ~/bin/ccode/headers -MD -Wimplicit -pg
```

## Table 22.4 Commonly used debugging options available for gcc during the compilation phase

| Option | Purpose | Value | Example |
| :--- | :--- | :--- | :--- |
| **-a** | Generates additional code grouping information for **gprof** | None | **-a** |
| **-ggdb** | Outputs debugging information in a format useful for GDB | None | **-ggdb** |
| **-pg** | Generates code in the format needed by **gprof**; you commonly need this item | None | **-pg** |
| **-print-file-name=** | Prints the full path to the library that would be used during the linking stage, and then stops | Library name | **-print-file-name=/usr/lib/printlib** |
| **-print-prog-name=** | Prints the full path to the program that would be used during the linking stage, and then stops | Program name | **-print-prog-name=cpp** |
| **-print-search-dirs** | Prints the names of the directories that gcc will search during the compilation | None | **-print-search-dirs** |
| **-Q** | Prints progress information, such as statistics and a list of the functions as they are compiled | None | **-Q** |
| **-save-temps** | Saves all temporary intermediate files so that you can examine them | None | **-save-temps** |

7. If the code you are compiling is going to produce a large program, you probably want to utilize some of the optimization parameters available for the compiler phase. See Table 22.5 for a brief list of the optimization parameters to choose from. The program you are setting up to compile in this example is not going to be huge. Use the lowest level of optimization, giving you the following:

```
gcc -I~/ccode/headers -MD -Wimplicit -pg -O0
```

8. You may find that you need to tell gcc explicitly where to find various types of files. Table 22.6 outlines the choices you have available. For this example, you do not need any of these options.

9. You are finally finished with compiler options. I assume that you are not trying to insert assembly code in with the C code, so now we move directly to the linking phase. Choose the options you want to use from Table 22.7. For the example, you do not need any of these options.

## Table 22.5 Commonly used optimization parameters available for gcc during the compilation phase

| Option | Purpose | Value | Example |
| :--- | :--- | :--- | :--- |
| **-O** | Takes the extra time and compilation resources to optimize the code | None | **-O** |
| **-O0** | Does not take the extra time and compilation resources to optimize the code | None | **-O0** |
| **-O2** | Optimizes the code more than would be done with just **-O** | None | **-O2** |
| **-O3** | Uses the highest level of optimization | None | **-O3** |
| **-Os** | Optimizes for size instead of speed | None | **-Os** |
