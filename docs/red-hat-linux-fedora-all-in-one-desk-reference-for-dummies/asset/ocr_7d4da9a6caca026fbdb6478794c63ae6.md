# Regular expressions

If you have used any UNIX or Linux system for a while, you probably know about the grep command, which enables you to search files for a pattern of strings. Following is a typical use of grep to locate all files that have any occurrences of the string blaster or Blaster — on any line of all files with names that end in .c:

```
cd /usr/src/linux*/drivers/cdrom
grep "[bB]laster" *.c
```

The preceding grep command finds all occurrences of blaster and Blaster in the files with names ending in .c.

The grep command's "[bB]laster" argument is known as a regular expression, a pattern that matches a set of strings. You construct a regular expression with a small set of operators and rules that resemble the ones for writing arithmetic expressions. A list of characters inside brackets ([...]), for example, matches any single character in the list. Thus, the regular expression "[bB]laster" is a set of two strings, as follows:

```
blaster  Blaster
```

Perl supports regular expressions, just as the grep command does. Many other Red Hat Linux programs, such as the vi editor and sed (the stream editor), also support regular expressions. The purpose of a regular expression is to search for a pattern of strings in a file. That's why editors support regular expressions.

You can construct and use complex regular expressions in Perl. The rules for these regular expressions are fairly simple. Essentially, the regular expression is a sequence of characters in which some characters have special meaning. Table 4-1 summarizes the basic rules for interpreting the characters used to construct a regular expression.

Table 4-1 Rules for Interpreting Regular Expression Characters

| Expression | Meaning |
|---|---|
| . | Matches any single character except a newline. |
| x* | Matches zero or more occurrences of the character x. |
| x+ | Matches one or more occurrences of the character x. |
| x? | Matches zero or one occurrence of the character x. |
| [...] | Matches any of the characters inside the brackets. |
| x{n} | Matches exactly n occurrences of the character x. |
| x{n,} | Matches n or more occurrences of the character x. |

(continued)