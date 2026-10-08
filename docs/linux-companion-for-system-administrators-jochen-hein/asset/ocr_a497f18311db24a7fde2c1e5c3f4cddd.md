# 324 TOOLS (NOT ONLY) FOR PROGRAMMERS

# 11.1 The make program

The program is primarily used for compilation of large programs that consist of many individual modules. When changes are made to the source code, only the modified program parts are recompiled. Compared to a complete compilation, this saves a lot of time; therefore the sources of nearly all programs are supplied with a Makefile which controls compilation.

GNU make uses one of the following files as control file for the compilation process, provided the file exists: Makefile, or Makefile. Other files can be specified by means of the option -f. If you use special functions of GNU make in your Makefile, you should name this file GNUMakefile.

At the call of make, the default target specified in the Makefile is created. If an additional parameter is specified, that target is created. Let us look at a simple example to explain this (Listing 11.1).

```
# A simple Makefile for prune
all: prune

prune: prune.c
	gcc -s prune.c -o prune

install: prune
	install -m 755 prune /usr/local/sbin/prune
	echo edit /etc/prune.conf to suit your system
```

Listing 11.1 A simple Makefile.

The make command creates the default target all. The default target is the first target in the Makefile. Targets are always written in the first column and terminated with a colon: there is a dependency on the file or target prune. Dependencies are written to the right of the column. Comments in Makefile begin with a hash sign (#) and end with the end of the line.

In the target prune which depends on the file prune, the C compiler is called if the file prune is more recent than the file prune. For this simple function, make already has a so called default rule that would be applied if no command was specified at this point. Commands are entered after a tab. If spaces are used instead of the tabs, it is possible some make versions show an error message.

The make install command executes the commands specified in the target install. First, however, it checks whether the program prune must be newly created. The install command copies the program to the location in the