# Understanding Perl Packages and Modules 801

The package provides a way to control the namespace — a term that refers to the collection of variable and subroutine names. Although you may not be aware of, when you write a Perl program, it automatically belongs to a package named main. Besides, other Perl packages are in the Perl library (in the /usr/lib/perl/X.Y.Z directory of Fedora Core system where X.Y.Z is the version number of Perl such as 5.8.3), and you can define your own package as well.

Perl modules are packages that follow specific guidelines.

# Perl packages

You can think of Perl package as a convenient way to organize a set of related Perl subroutines. Another benefit is that variable and subroutine names in a package do not conflict with names used elsewhere in the program. Thus, a variable $count in one package remains unique to that package and does not conflict with $count used elsewhere in a Perl.

A Perl package is in a single file. The package statement is at the beginning of the file to declare the file as a package and to give the package a name. For example, the file timelocal.pl defines a number of subroutines and variables in a package named timelocal.(Note that the Time:Local module supersedes the timelocal.pl file). The timelocal.pl file has the following package statement in various places:

```
package timelocal;
```

The effect of this package declaration is that all subsequent variable names and subroutine names are considered to be in the timelocal package. You can put such a package statement at the beginning of the file that implements the package.

What if you are implementing a package and you need to refer to a subroutine or variable in another package? As you might guess, you will need to specify both the package name and the variable (or subroutine) name. Perl provides the following syntax for referring to a variable in another package:

```
$Package::Variable
```

Here Package is the name of the package, and Variable is the name of the variable in that package. If you omit the package name, Perl assumes you're referring to a variable in the main package.

To use a package in your program, you can simply call the require function with the package filename as an argument. For example, a package named

Book IX
Chapter 4
Perl Programming