
difference whether the declaration occurs inside or outside the § function). The value that is returned by § is assigned to the global variable r inside d, which then returns back to m. Inside m, the value of the global variable r is displayed. This example, when run, produces a result of 4.0 at the terminal (because that’s obviously the square of 2.0).

Study the example until you feel comfortable with it. This small—albeit impractical—example illustrates very important concepts about communicating between modules, and it’s necessary that you understand these concepts to work effectively with larger programs.

## Using Header Files Effectively

In [Chapter 12, “The Preprocessor,”](#) you were introduced to the concept of the include file. As stated there, you can group all your commonly used definitions inside such a file and then simply include the file in any program that needs to use those definitions. Nowhere is the usefulness of the # facility greater than in developing programs that have been divided into separate program modules. If more than one programmer is working on developing a particular program, include files provide a means of standardization: Each programmer is using the same definitions, which have the same values. Furthermore, each programmer is thus spared the time-consuming and error-prone task of typing these definitions into each file that must use them. These last two points are made even stronger when you start placing common structure definitions, external variable declarations, typedef definitions, and function prototype declarations into include files. Various modules of a large programming system invariably deal with common data structures. By centralizing the definition of these data structures into one or more include files, you eliminate the error that is caused by two modules that use different definitions for the same data structure. Furthermore, if a change has to be made to the definition of a particular data structure, it can be done in one place only—inside the include file.

Recall your Date structure from [Chapter 8, “Working with Structures;”](#) following is an include file that might be similar to one you would set up if you have to work with a lot of dates within different modules: It is also a good example of how to tie together many of the concepts you’ve learned up to this point.

[Click here to view code image](#)

The header file defines two enumerated data types, `day` and `month` and the data structure `Date` (and note the use of the enumerated data types); uses `typedef` to create a type called `Date`; and declares functions that use this type, a macro to set a date to specific values (using compound literals), and an external variable called `today`, that will presumably be set to today's date (and is defined in one of the source files).

As an example using this header file, the following is a rewritten version of the `isLeapYear` function from Chapter 8.

[Click here to view code image](#)

## Other Utilities for Working with Larger Programs

As briefly mentioned previously, the IDE can be a powerful tool for working with larger programs. If you still want to work from the command line, there are tools you might want to learn how to use. These tools are not part of the C language. However, they can help speed your development time, which is what it's all about.

Following is a list of tools you might want to consider when working with larger programs. If you are running Unix, you will find a plethora of commands at your disposal that can also help you in your development efforts. This is just the tip of the iceberg here. Learning how to write programs in a scripting language, such as the Unix shell, can also prove useful when dealing with large numbers of files.

### The make Utility

This powerful utility (or its GNU version gmake) allows you to specify a list of files and their dependencies in a special file known as a Makefile. The make program automatically recompiles files only when necessary. This is based on the modification times of a file. So, if make finds that your source (.c) file is newer than your corresponding object (.o) file, it automatically issues the commands to recompile the source file to create a new object file. You can even specify source files that depend on header files. For example, you can specify that a module called `definitions.h` is dependent on its source file `definitions.c` as well as the header file `declarations.h`. Then, if you change anything inside the `declarations.h` header file, the make utility automatically recompiles the `definitions.c` file. This is based on the simple fact that the header file is newer than the source file.

Following is a simple Makefile that you could use for the three-module example from this chapter. It is assumed here that you’ve placed this file in the same directory as your source files.

```bash
$ cat Makefile
```

A detailed explanation of how this Makefile works is not provided here. In a nutshell, it defines the set of source files (SRC), the corresponding set of object files (OBJ), the name of the executable (PROG), and some dependencies. The first dependency,

```bash
$ PROG: $(OBJ)
```

says that the executable is dependent on the object files. So, if one or more object files change, the executable needs to be rebuilt. The way to do that is specified on the following gcc command line, which must be typed with a leading tab, as follows:

```bash
$  gcc $(OBJ) -o $(PROG)
```

The last line of the Makefile,

```bash
$ %.o: %.c $(DEPS)
```

says that each object file depends on its corresponding source file. So, if a source file changes, its corresponding object file must be rebuilt. The make utility has built-in rules that tell it how to do that.

Here’s what happens the first time you run make:

```bash
$ make
```

That’s kind of nice! make compiled each individual source file and then linked the resulting object files to create the executable.

If you instead had an error in `m`, here’s what the output from `make` would have looked like:

[Click here to view code image](#)

Here, make found there was an error in compiling `m` and stopped the make process, which is its default action.

If you correct `m` and run make again, here’s what happens:

[Click here to view code image](#)

Notice that make didn’t recompile `m`. That’s because it knew it didn’t have to. Therein lies the real power and elegance of the make utility.

Even with this simple example, you can use the sample Makefile to start using make for your own programs. Appendix E, “Resources,” tells you where you can turn for more information on this powerful utility.

### The cvs Utility

This is one of several utilities for managing source code. It provides for automatic version-tracking of source code, and keeps track of changes that are made to a module. This allows you to re-create a particular version of a program if needed (either to roll back code or to re-create an older version for customer support, for example). With cvs (which stands for Concurrent Versions System), you “check out” a program (using the cvs command with the checkout option), make your changes to it, and then “check it back in” (using the cvs command with the commit option). This mechanism avoids the potential conflict that can arise if more than one programmer wants to edit the same source file. With cvs, programmers can be at multiple locations and can all work on the same source code over a network.

### Unix Utilities: ar, grep, sed, and so on

A wide assortment of commands available under Unix makes large program development easier and more productive. For example, you can use `ar` to create your own library. This is useful, for example, if you create a bunch of utility functions that you frequently use or want to share. Just as you linked your program with the `-lm` option whenever you used a routine from the standard math library, so too can you specify your own library at link time, using the `-l` option. During the link edit phase, the library is automatically searched to locate functions that you reference from the library. Any such functions are pulled from the library and linked together with your program.

Other commands such as `grep` and `sed` are useful for searching for strings in a file or making global
