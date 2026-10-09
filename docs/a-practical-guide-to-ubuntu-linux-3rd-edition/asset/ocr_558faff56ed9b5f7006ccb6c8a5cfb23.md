the keyword **my**, in which case it is a lexical variable (page 1045) that is defined only within the block or file it appears in. See “Subroutines” on page 1071 for a discussion of the locality of Perl variables.

# ## Lexical variables overshadow package variables

> caution
> If a lexical variable and a package variable have the same name, within the block or file in which the lexical variable is defined, the name refers to the lexical variable and not to the package variable.

A Perl variable comes into existence when you assign a value to it—you do not need to define or initialize a variable, although it may make a program more understandable to do so. Normally, Perl does not complain when you reference an uninitialized variable:

```
$ cat variablel.pl
#!/usr/bin/perl
my $name = 'Sam';
print "Hello, $nam, how are you?\n"; # Typo, e left off of name

$ ./variablel.pl
Hello, , how are you?
```

**use strict**
Include **use strict** to cause Perl to require variables to be declared before being assigned values. See the **perldleb** but **man** page for more information. When you include **use strict** in the preceding program, Perl displays an error message:

```
$ cat variablelb.pl
#!/usr/bin/perl
use strict;
my $name = 'Sam';
print "Hello, $nam, how are you?\n"; # Typo, e left off of name

$ ./variablelb.pl
Global symbol "$nam" requires explicit package name at ./variablelb.pl line 4.
Execution of ./variablelb.pl aborted due to compilation errors.
```

# ## Using my: lexical versus package variables

> tip
> In **variablel.pl**, **$name** is declared to be lexical by preceding its name with the keyword **my**; its name and value are known within the file **variablel.pl** only. Declaring a variable to be lexical limits its scope to the block or file it is defined in. Although not necessary in this case, declaring variables to be lexical is good practice. This habit becomes especially useful when you write longer programs, subroutines, and packages, where it is harder to keep variable names unique. Declaring all variables to be lexical is mandatory when you write routines that will be used within code written by others. This practice allows those who work with your routines to use whichever variable names they like, without regard to which variable names you used in the code you wrote.
> 
> The shell and Perl scope variables differently. In the shell, if you do not **export** a variable, it is local to the routine it is used in (page 992). In Perl, if you do not use **my** to declare a variable to be lexical, it is defined for the package it appears in.