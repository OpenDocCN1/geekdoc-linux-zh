+   ■ **objcopy** Used to copy and convert object files. objcopy is used to convert object files from one type to another, such as from bdf to elf.

+   ■ **objdump** Used to display the contents of a binary file. This is useful for developers who are concerned about the actual contents and format of their object files, as well as the function of their code.

+   ■ **ranlib** Generates an index to archive contents. The ranlib utility will take an object library and create an index of symbols so you can find which object in the library has the symbol you are looking for.

+   ■ **size** Lists the section and total sizes of object files. The output displays the various sizes of different parts of your code, such as text and data segments, as well as the size of the bss section of the code.

+   ■ **strings** Lists printable strings within files. This is very helpful if you are looking for a particular object file that has displayed an error message.

+   ■ **strip** Discards symbols from files. It can be used both for size considerations as well as for security.

+   ■ **readelf** Displays information about ELF format files. This is similar to objdump except that it works with ELF files.

Though the binutils may be of no use to many of you, they serve an important purpose when it comes to software development and debugging. This is especially true if you are only planning on running Oracle.

# ## The make Utility

The make utility is used to create binary files from source files and object files based on a template, or makefile. The makefile is used to define dependencies between source files, object files, and executables. These relationships, as well as methods of creating various dependent files, are used to create binaries. For example, the following relationships can be set up within a makefile:

```
```
test relies on test.o
test is created by linking test.o with lib.a
test.o relies on test.c
test.o is created by running gcc on test.c
```
```

This is just a description and does not represent the actual syntax of the makefile and the make utility.