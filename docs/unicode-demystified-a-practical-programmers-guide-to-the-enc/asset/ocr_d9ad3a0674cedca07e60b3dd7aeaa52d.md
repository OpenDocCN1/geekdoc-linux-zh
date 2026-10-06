With this command, the C preprocessor encounters the #include directive
in the file deriv.c file, it look for eqns.h in the subdirectory myincludes of the work-
ing directory.

# Use Relative Pathnames for Include Files

Using absolute pathnames for include files does not work if the location of the header file within the-
system changes. Using relative pathnames for header files works as long as the location of the header
file relative to the working directory remains the same.Relative pathnames also work with the -I
option on the gcc command line and allow header files to be moved.

Above the definition of the function main is a function prototype, a declaration
that tells the compiler what a function returns, how many arguments a func-
tions, and what the types of arguments are. In tabs.c the prototype for
function findstop informs the compiler that findstop returns type int and that it
expects a single argument of type pointer to int. Once the compiler has seen this
declaration, it can detect and flag inconsistencies in the definition and uses of
function.

For example, suppose that the reference to findstop in tabs.c were replaced with
the following statement:

```
inc = findstop();
```

The prototype for findstop would cause the compiler to detect a missing argument
an an error message. The programmer could then easily fix the problem.
When a function is present in a separate file or is defined after it is referenced
in a source file (as findstop is in the example), the function prototype helps the com-
piler that the function is being called properly. Without the prototype, the
compiler would not issue an error message, and the problem would manifest itself
as unexpected behavior during execution. At this late point, finding the bug mighte difficult and time-consuming.

Although you can call most C functions anything you want, each program must
h exactly one function named main. The function main is the control module:
Your program begins execution with the function main, which typically calls other
functions in turn, which may call yet other functions, and so forth. By putting-
different operations into separate functions, you can make a program easier to read
and maintain. The program in Figure 16-1 uses a function, findstop, to compute the
distance to the next stop. Although the few statements of findstop could easily
have been included in the main function, isolating them in a separate function
draw attention to a key computation.