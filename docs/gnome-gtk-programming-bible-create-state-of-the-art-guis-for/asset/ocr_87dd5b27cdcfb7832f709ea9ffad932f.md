# Summary

The setup to get automatic compilation to work is a bit involved, but the rewards come later as you develop your software. All of the dependencies among your source files are tracked automatically, and a correct and complete set of commands is used to compile and link your programs. As explained in detail in this chapter, the following is a list of the steps to take:

+   - Create a development directory containing the appropriate collection of files and directories. It also should include a copy of the macros distributed with the GNOME development software.

+   - Create the `configure.in` file that contains, by using macros, a basic description of your project. Also, create the `acconfig.h` file to be used as a template in creating `config.h`.

+   - Create a simple `autogen.sh` script you can use to find the dependencies and generate the make files.

+   - Create a `Makefile.am` file listing the names of the source files to be used as input, and the names of the object files to be generated. One of these appears in every directory in the development tree.

The next two chapters are for reference. Chapter 21 contains a list of the widgets of GTK+, and Chapter 22 contains a list of the widgets of GNOME. Many of these have been used in programs earlier in the book but, for those that haven't, there are small examples.