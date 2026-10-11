# The argument is John

This command is used to lock the password of the user John on the Linux system.

It is useful to know which options go with which commands to be efficient on the command line. The --help option with any command will give you a list of options that can be used with that particular command. It is not important to know every option by heart. The list also gives you a description of what the option does.

Let us see an example of this with the grep command. The grep command is used to search through a string or a file. If the file has a string that matches the one specified by you in your grep command, the output shows every line of the file that contains the specified string.

```
```
[student@desktop ~]$ grep --help

Usage: grep [OPTION]... PATTERN [FILE]...

Search for PATTERN in each FILE or standard input.

PATTERN is, by default, a basic regular expression (BRE).

Example: grep -i 'hello world' menu.h main.c

Regex Selection and Interpretation:

-E, --extended-regexp         PATTERN is an extended regular
expression (ERE)
-F, --fixed-strings           PATTERN is a set of newline-separated fixed
strings
-G, --basic-regexp           PATTERN is a basic regular expression
(BRE)
-P, --perl-regexp           PATTERN is a Perl regular expression
-e, --regexp=PATTERN        use PATTERN for matching
-f, --file=FILE             obtain PATTERN from FILE
```
```