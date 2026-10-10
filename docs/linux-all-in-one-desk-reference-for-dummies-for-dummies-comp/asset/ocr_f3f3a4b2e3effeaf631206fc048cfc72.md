# Perl packages

You can think of a Perl package as a convenient way to organize a set of related Perl subroutines. Another benefit is that variable and subroutine names defined in a package do not conflict with names used elsewhere in the program. Thus, a variable named `$count` in one package remains unique to that package and does not conflict with a `$count` used elsewhere in a Perl program.

A Perl package is in a single file. The package statement is used at the beginning of the file to declare the file as a package and to give the package a name. For example, the file *ctime.pl* defines a number of subroutines and variables in a package named *ctime*. The *ctime.pl* file has the following package statement in various places:

```
```perl
package ctime;
```
```

The effect of this package declaration is that all subsequent variable names and subroutine names are considered to be in the *ctime* package. You can put such a package statement at the beginning of the file that implements the package.

What if you implement a package and you need to refer to a subroutine or variable in another package? As you might guess, all you need to do is specify both the package name and the variable (or subroutine) name. Perl provides the following syntax for referring to a variable in another package:

```
```perl
$Package::Variable
```
```

Here *Package* is the name of the package, and *Variable* is the name of the variable in that package. If you omit the package name, Perl assumes that you’re referring to a variable in the *main* package. Note that C++ happens to use a similar syntax when referring to variables in another C++ class. (A class is basically a collection of data and functions— a template for an object.)

To use a package in your program, you can simply call the `require` function with the package filename as an argument. For example, a package named *ctime* is defined in the file *ctime.pl*. That package includes the *ctime* subroutine that converts a binary time into a string. The following simple program uses the *ctime* package from the *ctime.pl* file:

```
```perl
#!/usr/bin/perl -w
# Use the ctime package defined in ctime.pl file
require 'ctime.pl';
# Call the ctime subroutine
$Time = ctime(ctime());
# Print the time string
print $Time;
```
```