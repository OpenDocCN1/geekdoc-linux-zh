The variable `helloauto_SOURCES` specifies the source files that are used to build the binary output file named `helloauto`. Using this information, the make file is generated to check all of these files for dependencies.

The variable `helloauto_LDAAD` specifies a list of libraries that are searched to resolve external references in the files that make up `helloauto`.

You can add other programs to the same file by adding its name to the list in `bin_PROGRAMS`, and adding a new `SOURCE` and `LDAAD` entry for it. Also, if you wish to have subdirectories of source files, you can use a `SUBDIRS` definition to point to the right directory. This means that to add a new directory to your source tree, you simply create a `Makefile.am` file in the new source directory and add a `SUBDIRS` entry in the `Makefile.am` of the parent directory.

# Running the `autogen.sh` Script

There are two steps required to compile everything. First, the script is run from your root development directory like this:

```
autogen.sh
```

This adds a number of files to your root development directory. Exactly what files are added depends largely on the settings and choices you made earlier. For example, if you use `ALL_LINGUAS` to set up some translation, the subdirectories `po` and `intl` are created to hold translation strings.

After the script runs, simply enter:

```
make
```

This command compiles and links everything in the entire directory tree. If you are in any of the source subdirectories, entering `make` only compiles that current directory and those below it.

The make files compare the dates on the source to the dates on the object files, so if you compile again, only the changed files are included. However, you can force a complete recompilation by removing the object files. To delete all the object files, along with any other files that are created during the compile, enter:

```
make clean
```

As you develop your application and add new source files, you will need to update the appropriate `Makefile.am` file and then execute `autogen.sh` to include the new source file.

After you have a successful compile, you can install the executable files with:

```
make install
```