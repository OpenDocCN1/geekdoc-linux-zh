Perl statements are terminated with a semicolon. A Perl statement can extend over several actual screen lines because Perl is not concerned about whitespace.

The second line of the simple program prints the text enclosed in quotation marks. \n is the escape sequence for a newline character.

# TIP

Using the perldoc and man commands is an easy way to get more information about the version of Perl installed on your system. To learn how to use the perldoc command, enter the following:

```
$ perldoc perldoc
```

To get introductory information on Perl, you can use either of these commands:

```
$ perldoc perl
```

```
$ man perl
```

For an overview or table of contents of Perl's documentation, use the perldoc command like this:

```
$ perldoc perltoc
```

The documentation is extensive and well organized. Perl includes a number of standard Linux manual pages as brief guides to its capabilities, but perhaps the best way to learn more about Perl is to read its perlfun c document, which lists all the available Perl functions and their usage. You can view this document by using the perldoc script and typing perldoc perlfun c at the command line. You can also find this document online at http://www.cpan.org/doc/manual/html/pod/perlfun c.html.

# Perl Variables and Data Structures

Perl is a weakly typed language, meaning that it does not require that you declare a data type, such as a type of value (data) to be stored in a particular variable. C, for example, makes you declare that a particular variable is an integer, a character, a structure, or whatever the case may be. Perl variables are whatever type they need to be, and can change type when you need them to.

# Perl Variable Types