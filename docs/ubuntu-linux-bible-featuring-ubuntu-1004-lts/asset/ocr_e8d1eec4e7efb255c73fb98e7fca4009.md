# Part II: Ubuntu for Desktop Users

The first line identifies the binary target (hello) that this Makefile builds, and the fact that this binary must be regenerated whenever the source file hello.c is modified. The second line (which begins with a tab) specifies the command necessary to produce binary target. To invoke Makefile, you simply execute the make command in the directory containing the Makefile. The make program automatically looks for a file named Makefile and builds any rules that it contains.

# Tip

The fact that all lines containing a build rule must begin with a tab is one of the most common problems with handcrafted Makefiles. 

Although this example shows the true basics of a Makefile, it is also a trivial example that doesn't show any of the real benefits that Makefiles can provide in simplifying and automating compilation and recompilation. Let's consider another example. In the previous section, one of the examples I compiled a single binary from two object modules, using the following command lines:

```
$ gcc -c showdate.c
$ gcc -c helper.c
$ gcc showdate.o helper.o -o showdate
```

A Makefile for this application would look something like the following:

```
showdate.o helper.o
gcc showdate.o helper.o -o showdate
```

```
showdate.o: showdate.c
gcc -c showdate.c
helper.o: helper.c
gcc -c helper.c
```

This example highlights how a Makefile can reduce the amount of recompilation necessary when you have only modified some of the files associated with a project. For example, this Makefile states that the showdate binary depends on the two object modules showdate.o and helper.o, and provides a rule for generating the binary by using gcc to link the two object files. It continues to highlight that each of these object modules depends on its C language file, and provides a rule for using gcc to regenerate each of the object modules.

This Makefile can simplify recompilation if, for example, only one of the C files was modified. The Makefile would regenerate the object module for only the C file that has been modified, and relink the existing object file with the new object file to regenerate the binary.

As your projects grow larger, you will want to take advantage of other Makefile features, such as defining and using variables, using some cryptic symbols to simplify make rules, and so on. Some good sources for more advanced information about the make program and Makefiles are the:

+   * www.linuxdevcenter.com/pub/a/linux/2002/01/31/make_intro.html: A nice article on using make from O'Reilly & Associates Linux Development Center