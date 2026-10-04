# Getting an Overview of Perl

# Regular expressions

If you used any UNIX or Linux system for a while, you probably know about the grep command, which enables you to search for files by a pattern of strings. Following is a typical use of grep:

```
cd /usr/src/linux*/drivers/cdrom
grep [bB]laster *.c
```

The preceding grep command finds all occurrences of blaster and Blaster in the names ending in .c.

The grep command's [bB]laster argument is known as a regular expression, a pattern that matches a set of strings. Construct a regular expression with a small set of operators and rules that resemble the ones inside brackets ([...]), for writing atomic expressions. A list of characters, for example, matches any single character in the list. Then, the regular expression [bB]laster is a set of two strings, as:

blaster  Blaster

Perl supports regular expressions, just as the grep command does. Many other Fedora programs, such as the vi editor and sed editor, also support regular expressions. The purpose of a regular expression is to search for strings in a file. That's why editors support regular expressions.

You can construct and use complex expressions in Perl. The rules for these regular expressions are fairly simple. Essentially, the regular expression is a sequence of characters in which some characters have special meaning. Table 4-1 summarizes the basic rules for interpreting the characters used to construct a regular expression.

| Table 4-1 | Rules for Interpreting Regular Expression Characters |
| --- | --- |
| x* | Matches any single character except a newline. |
| x+ | Matches one or more occurrences of the character x. |
| x? | Matches zero or one occurrences of the character x. |
| [...] | Matches any of the characters inside the brackets. |
| x(n) | Matches exactly n occurrences of the character x. |
| x(n,) | Matches n or more occurrences of the character x. |
| x(,m) | Matches zero or, at most, m occurrences of the character x. |

(continued)