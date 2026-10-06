(usually compile and/or link) the target file. The make utility executes the construction-commands when the modification time of one or more of the files in the prerequisite-list is more recent than that of the target file.

The following example shows the dependency line and construction commands for the file name in Figure 16-3. The example depends on the prerequisites size.o and length.o. An appropriate gcc command constructs the target:

```
form: size.o length.o
TAB gcc -o form size.o length.o
```

Each of the prerequisites on one dependency line can be a target on another dependency line. For example, size.o and length.o are on other dependency lines. Although the example in Figure 16-3 is simple, the nesting of dependency specifications can create a complex hierarchy that specifies relationships among many files.

The following make (named Makefile) corresponds to the complete dependency graph shown in Figure 16-3. The executable form depends on two object files, and the objects each depend on their source files and a header file, form.h. In turn, form depends on two other header files:

```
$ cat Makefile
form: size.o length.o
gcc -o form size.o length.o
size.o: size.c form.h
gcc -c size.c
length.o: length.c form.h
gcc -c length.c
form.h: num.h table.h
cat num.h table.h > form.h
```

Although the last line would not normally be seen in a makefile, it illustrates the fact that you can put any shell command on a construction line. Because files are processed by the shell, the command line should be one that you could input in response to a shell prompt.

The following command builds the default target form if its prerequisites are more recent or if the target does not exist:

```
$ make
```

Thus, if the file form has been deleted, make will rebuild it, regardless of the modification dates of its prerequisite files. The first target in amakefile is the default and is built when you call make without any arguments.

If you want make to rebuild a target other than the first in the makefile, you must provide the target as an argument to make. The following command rebuilds form.h if it does not exist or if its prerequisites are most recent:

```
$ make form.h
```