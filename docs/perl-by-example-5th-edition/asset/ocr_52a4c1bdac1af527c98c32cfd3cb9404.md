# EXAMPLE 4.23

```
```perl
 (The Script)
1   use warnings;
2   print "What is your name? ";
3   chomp($name = <STDIN>);
4   print "$nime, welcome!\n";  # Misspelled $name

        # Scriptname: warwne

(Output)
Name "main::name" used only once: possible typo at warwne.plx line 3.
Name "main::nime" used only once: possible typo at warwne.plx line 4.
What is your name? Joe Shmoe
Use of uninitialized value $nime in concatenation (.) or string at warwne.
plx line 4, <STDIN> line 1.
, welcome!
```
```

# EXPLANATION

In Perl versions 5.6 and later, you can use the warnings pragma instead of the -w switch. The -w switch produced warnings for the entire script, whereas the warnings pragma can be limited to the enclosing block. When you say use warnings, that tells Perl that you want to use a module called warnings.pm from the Standard Perl Library. If you want to turn warnings off, just type no warnings on a line by itself.

The variable $nime is a misspelling. It should have been spelled $name. Perl lets you know by saying you only used the variable once in the string. The program still runs, but the string is missing the value of $name.

# 4.5.3  The diagnostics Ppragma

This special pragma enhances the warning messages to a more verbose explanation of what went wrong in your program. Like the warnings pragma, it affects the compilation phase of your program, but unlike the warnings pragma, it attempts to give you an explanation that doesn't assume you are an experienced programmer.

# EXAMPLE 4.24

```
```perl
 (The Script)
1   use diagnostics;
2   print "Hello there!";  # Unmatched quote
3   print "We are on line number ", _LINE_,"\n";
```
```