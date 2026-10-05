Within a string enclosed between double quotation marks, a backslash escapes (quotes) another backslash. Thus Perl displays "\n" as \n. Within a regular expression, Perl does not expand a metacharacter preceded by a backslash. See the string.l program on the previous page.

As in the shell, a comment in Perl begins with a hashmark (#) and ends at the end of the line (just after the newline character).

Table 28-1 shows some of the characters that are special strings in Perl. Perl interpolates these characters when they appear between double quotation marks but not when they appear between single quotation marks. Table 28-3 on page 176 lists metacharacters, which are special within regular expressions.

# Table 28-1 Some special characters

| Character | When within double quotation marks, interpolated as |
| \0 (zero) | The ASCII character whose octal value is xx |
| \a | An alarm (bell or beep) character (ASCII 7) |
| \e | An ESCAPE character (ASCII 27) |
| \n | A NEWLINE character (ASCII 10) |
| \r | A RETURN character (ASCII 13) |
| \t | A TAB character (ASCII 9) |

# VARIABLES

Human languages, Perl distinguishes between singular and plural data. Strings and numbers are singular; lists of strings or numbers are plural. Perl provides three types of variables: scalar (singular), array (plural), and hash (plural); also called associative arrays. Perl identifies each type of variable by a special character preceding it. The name of a scalar variable begins with a dollar sign ($), an array variable begins with an at (@), and a hash variable begins with a percent sign (%). As opposed to the way the shell identifies variables, Perl requires the character to appear each time you refer a variable, including when you assign a value to the variable:

```
$ name="Zach"; echo "$name"
Zach
```

```
$ perl -e 'name=Zach; print "$name\n";' (perl)
Zach
```

Variable names, which are case sensitive, can include letters, digits, and the underscore character (_). A Perl variable is a package variable (page 1045) unless it is preceded by