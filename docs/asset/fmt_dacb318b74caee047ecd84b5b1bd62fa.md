
`make` is the standard utility for building programs. It can be very difficult in large programs, with many source-code files, to keep track of which files have been changed and need to be compiled and which files need only to be linked. The `make` utility will do this for you.

`make` was designed for a development environment in which different source-code files in a program are constantly modified. `make` keeps track of which source files have been changed and which have not. It recompiles those that have been changed, linking them with the rest of the object-code files to create a new executable file.

In the next example, the user enters the command `make` on the command line to invoke the `make` utility. `make` then compiles those files that have recently been modified and creates a new executable file. `make` displays each Linux command it executes.
