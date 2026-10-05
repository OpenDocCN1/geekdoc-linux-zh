
# 1044 CHAPTER 28 THE PERL SCRIPTING LANGUAGE

You can use perdoc to display the documentation:

$ perdoc pod.ex1.pl
POD.EX1(1) User Contributed Perl Documentation POD.EX1(1)

# A Perl Program to Say Hi.

This simple Perl program includes documentation in pod format. The following =cut command tells perdoc what follows is not documentation.

# pod Documentation Resumes with any pod Command

See the perdoc.org/perpod.html page for more information on pod and perdoc.perl for complete Perl documentation.

# perl v5.10.0 2008-10-14 POD.EX1(1)

Most widely distributed modules and scripts, as well as Perl itself, include embedded pod-format documentation. For example, the following command displays information about the Perl print function:

```
$ perdoc -f print
FILEHANDLE LIST
print LIST
print Prints a string or list of strings. Returns true if successful. FILEHANDLE may be a scalar variable name, in which case the variable contains the name or a reference to the file-handle, introducing one level of indirection. (NOTE: If FILEHANDLE is a variable and the next token is a term, it may ...
```

Once you have installed a module (page 1079), you can use perdoc to display documentation for that module. The following example shows perdoc displaying information on the locally installed Timestamp::Simple module:

# $ perdoc Timestamp::Simple

Timestamp::Simple(3) User Contributed Perl Documentation Timestamp::Simple(3)

NAME

Timestamp::Simple - Simple methods for timestamping

SYNOPSIS

```
use Timestamp::Simple qw(stamp);
print stamp, "\n";...
```

Give the command man perdoc or perdoc perdoc to display the perdoc man and read more about this tool.

# Make Perl programs readable

Although Perl has many shortcuts that are good choices for one-shot programming, the code in this chapter presents code that is easy to understand and easy to maintain.

# INTRODUCTION TO PERL 1045

# TERMINOLOGY

This section defines some of the terms used in this chapter.

- Module A Perl module is a self-contained chunk of Perl code, frequently containing several functions that work together. A module can be called from another module or from a Perl program. A module must have a unique name. To help ensure names, Perl provides a hierarchical namespace (page 1161) for modules, separating components of a name with double colons (::). Example names are Timestamp::Simple and WWW::Mechanize.

- Distribution A Perl distribution is a set of one or more modules that perform a task. You can search for distributions and methods at search.cpan.org. Examples of distributions including Timestamp-Simple (the Timestamp-Simple-1.01.tar.gz archive file contains the Timestamp::Simple (simple module only) and WWW-Mechanize (WWW-Mechanize-1.34.tar.gz contains the WWW::Mechanize module, plus supporting modules including WWW::Mechanize::Link and WWW::Mechanize::Image)

- Package A package defines a Perl name. For example, in the variable with the name WWW::Mechanize::ex, is a scalar variable in the WWW::Mechanize package, where “package” is used in the sense of a namespace. Using the same name, as WWW::Mechanize, for a distribution, a package, can be confusing.

- Block A block is zero or more statements, defined by curly braces ({}), that defines a scope. The shell control syntax explanations refer to these elements as commands. See the if...then control structure on page 954 for an example.

- Variable A package variable is defined within the package it appears in. Other packages refer to package variables by using the variable's fully qualified name (for example, SText::Wrap::columns). By default, variables unless define them as lexical variables.

- Lexical A lexical variable, which is defined by the name of a variable with the keyword my (see the tip on page 1050), is defined only within the block or file it appears in. Other languages refer to lexical variable as a local variable. Because Perl 4 used the lexical keyword with a different name, Perl 5 uses the lexical in in its place. When programming bash, variables that are not exported (page 992)

- List A list is a series of zero or more scalars. The following list has three elements—two numbers and a string:

(2, 4, 'Zach')

- Array An array is a variable that holds a list of elements in a defined order. The following line of code, @a is an array. See page 1053 for information about array variables.

```
@a = (2, 4, 'Zach')
```

- Compound A compound statement is made up of other statements. For example, if the if statement (page 1057) incorporates an statement that normally includes other statements within the block it controls.

# RUNNING A PERL PROGRAM

There are several ways you can run a program written in Perl. The -e option enables you to enter a program on the command line:

```
$ perl -e 'print Hi.\n'
Hi there.
```

The -e option is a good choice for testing Perl syntax and running brief, one-shot programs. This option requires that the Perl program appear as a single argument on the command line. The program must immediately follow this option—it is easy to write this type of program to include the program within single quotation marks.

Because Perl is a member of the class of utilities that take input from a file or standard input (page 24), you can run a script by passing the filename as an argument. The most common way is to use a shebang line, like #!usr/bin/perl, at the beginning of the file. This tells the shell to use the Perl interpreter to execute the script. The file must be made executable, which is typically done with the chmod +x command.

```perl
#!/usr/bin/perl
print "Hi there.\n";
```

```
$ ./script.pl
Hi there.
```

Alternatively, you can run the script by calling the interpreter directly:

```
$ perl script.pl
Hi there.
```

The -e option allows you to run Perl code directly from the command line:

```
$ perl -e 'print "Hi there.\n"'
Hi there.
```

This is a good choice for testing Perl syntax and running brief, one-shot programs. This option requires that the Perl program appear as a single argument on the command line. The program must immediately follow this option—it is easy to write this type of program to include the program within single quotation marks.

# PERL VERSION 5.10

All examples in this chapter were run under Perl 5.10. Give the following command to see which version of Perl the local system is running:

```
$ perl -v
```

This is perl, v5.10.0 built for i486-linux-gnu-thread-multi

use feature 'say' The say function is a Perl 6 feature that is available in Perl 5.10. It works the same way as print, except it adds a newline (\n) at the end of each line. Some versions of Perl require you to use explicitly that you want to say. The use function in the following example tells Perl to enable say. Running this program without the use line to see if the local version of Perl requires it.

```
$ cat 5.10.pl
use feature 'say';
say 'Output by say.';
print 'Output by print.';
say 'End.'
$ perl 5.10.pl
Output by say.
print Output by print.End.
```

Early versions If you are running an earlier version of Perl, you will need to replace say in the Perl examples in this chapter with print and terminate the print statement with a quoted \n:

```
$ cat 5.8.pl
print 'Output by print in place of say.', "\n";
print 'Output by print.';
say 'End.', "\n";
```

```
$ perl 5.8.pl
Output by print of say.
print Output by print.End.
```

# SYNTAX

Statements A Perl program comprises one or more statements, each terminated by a semicolon (;). These statements are free-form with respect to whitespace (page 1180), except for whitespace within quoted strings. Multiple statements can appear on a single line, terminated by a semicolon. The following programs are equivalent. The first occupies two lines, the second only one; look at the differences in the spacing around the equal and plus signs. See use feature 'say' (above) if these programs complain about say not being available.
