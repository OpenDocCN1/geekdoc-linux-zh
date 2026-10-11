
## EXPLANATION

- 1. The scalar variable $num is assigned the value 5.
- 2. The array is assigned three colors. The @ is a special character used to create a list of values. The @ is interpreted within double quotes.
- 3. The string is enclosed in double quotes. The value of the scalar variable is printed. The string literal, \n, is interpreted.
- 4. The @ is evaluated and the array of values is printed.
- 5. The dollar sign ($) is printed as a literal dollar sign when preceded by a backslash; in other words, variable substitution is ignored.
- 6. The special literals \t and \n are interpreted when enclosed within double quotes.

**Single Quotes**. If a string is enclosed in single quotes, it is printed literally (what you see is what you get). If a single quote is needed within a string, then it can be embedded within double quotes or backslashed. If double quotes are to be treated literally, they can be embedded within single quotes.

## EXAMPLE 4.4

```perl
(The Script)
use warnings;
# Single quotes
1 print 'I need $100.00.', "\n";
2 print 'The string literal, \\t, is used to represent a tab.', "\n";
3 print 'She cried, "Help me!"', "\n";
```

```text
(Output)
1 I need $100.00.
2 The string literal, \\t, is used to represent a tab.
3 She cried, "Help me!"
```

## EXPLANATION

- 1. The dollar sign is interpreted literally. In double quotes, it would be interpreted as a scalar. The \n is in double quotes in order for backslash interpretation to occur.
- 2. The string literal, \t, is not interpreted to be a tab but is printed literally.
- 3. The double quotes are protected when enclosed in single quotes (that is, they are printed literally).

**Backquotes**. UNIX/Windows' commands placed within backquotes are executed by the shell, and the output is returned to the Perl program as a string, usually assigned to a variable or made part of a *print* string. When the output of a command is assigned to a variable, the context is scalar (that is, a single value is assigned).[^4] For command substitution to take place, the backquotes cannot be enclosed in either double or single quotes. (Make note: UNIX shell programmers: backquotes cannot be enclosed in double quotes as in shell programs.)

> 3. If using other operating systems, such as Microsoft or Mac OS 9.1 and below, the OS commands available for your system will differ.

## EXAMPLE 4.5

```perl
(The Script for Unix/Linux)
use warnings;
# Backquotes and command substitution
1  print "The date is `date`.\n";
2  print "The date is `date`\n";       # Backquotes treated literally
3  $directory=`pwd`;                    # Windows users: `cd`
4  print "The current directory is $directory.\n";
```

```text
(Output)
1  The date is Mon Jun 25 17:27:49 PDT 2014.
2  The date is `date`.
3  The current directory is /home/jody/ellie/perl.
```

## EXPLANATION

- 1. The UNIX `date` command will be executed by the shell, and the output will be returned to Perl’s `print` string. The output of the `date` command includes the newline character. For Windows users, the command is `date /T`.
- 2. Command substitution will not take place when the backquotes are enclosed in single or double quotes.
- 3. The scalar variable `$directory`, including the newline, is assigned the output of the UNIX `pwd` command (that is, the present working directory). For Windows users, the command is `cd`.
- 4. The value of the scalar, `$directory`, is printed to the screen.

## Perl’s Alternative Quotes

Perl provides an alternative form of quoting—the `q`, `qq`, `qx`, and `qw` constructs.

- The `q` represents single quotes.
- The `qq` represents double quotes.
- The `qx` represents backquotes.
- The `qw` represents a quoted list of words. (See Table 4.1.)

### Table 4.1 Alternative Quoting Constructs

| Quoting Construct | What It Represents |
| :--- | :--- |
| `q/Hello/` | `'Hello'` |
| `qq/Hello/` | `"Hello"` |
| `qx/date/` | `` `date` `` |
| `@list=qw/red yellow blue;/` | `@list=('red', 'yellow', 'blue');` |

The string to be quoted is enclosed in **forward slashes**, but you can use alternative delimiters for all four of the *q* constructs. You can use a nonalphabetic character for the delimiter, such as a # sign, ! point, or paired characters, such as parentheses, square brackets, and so forth. You can also use a single character or paired characters. For example:

q/Hello/
q#Hello#
q(Hello)
q[Hello]
q{Hello}
q(Hello)

## EXAMPLE 4.6

```perl
(The Script)
use warnings;
# Using alternative quotes
1 print 'She cried, "I can't help you!"', "\n"; # Clumsy
2 print qq/She cried, "I can't help you!"\n/; # qq for double quotes
3 print q(I need $5.00\n); # Really need single quotes
4 print q(I need $5.00\n); # For a literal dollar sign to print
5 print qq(I need \$5.00\n); # What about backslash interpretation?
6 print qq/\n/, q/I need $5.00/, "\n";
7 print qq/The present working directory is /, qx(pwd);
8 print qq/Today is /, qx(date +%H); # Use qx(date +# (Windows)
9 print "The hour is ", qx(date +%H); # Unix only
```

```text
(Output)
1 She cried, "I can't help you!"
2 She cried, "I can't help you!"
3 I need .00
4 I need $5.00\nI need $5.00
5 I need $5.00
6 I need $5.00
7 The present working directory is /home/jody/ellie/perl
8 Today is Mon Jun 25 17:29:34 PDT 2014
9 The hour is 17
```

## 4.3 The print Function

## EXPLANATION

The string is enclosed in single quotes. This allows the conversational quotes to be printed as literals. The single quote in `can't` is quoted with a backslash so that it will also be printed literally. If it were not, it would be matched with the first single quote. The ending single quote would then have no mate, and, alas, the program would either tell you that you have a runaway quote or search for its mate until it reached the end of file unexpectedly.

The `qq` construct replaces double quotes. Now parentheses delimit the string. Because the `qq` is used, the dollar sign ($) in $5.00 is interpreted as a scalar variable with a null value. The .00 is printed. (This is not the way to handle your money!) The single `q` replaces single quotes. The $5 is treated as a literal. Unfortunately, so is the \n because backslash interpretation does not take place within single quotes. Without a newline, the next line is run together with line 4. In the next line, if the dollar sign is preceded by a backslash, the backslash "escapes" the special meaning of the $. Now the string will print correctly.

The \n is double quoted with the `qq` construct, the string *I need $5.00* is single quoted with the `q` construct, and old-fashioned double quotes are used for the second \n.

An alternative delimiter, the exclamation point (!), is used with the `q` construct (instead of the forward slash) to delimit the string.

The string *The present working directory* is enclosed in double quotes; the UNIX command `pwd` is enclosed in backquotes for command substitution. The `qq` construct quotes *Today*; the `qx` construct replaces the backquotes used for command substitution. Note: To get the same results for MS-DOS, the date command takes the `/T` option. A different delimiter is used because of the slash in `/T`. Typing `q\date//T` would produce an error, so change the delimiter to something else, in this case a #.

Alternative delimiters, the curly braces, are used with the `qx` construct (instead of the forward slash). The output of the UNIX `date` command is printed.

Quoting rules affect almost everything you do in Perl, especially when printing a string of words. Strings are normally delimited by a matched pair of either double or single quotes. When a string is enclosed in single quotes, all characters are treated as literals. When a string is enclosed in double quotes, however, *almost* all characters are treated as literals, with the exception of those characters that are used for variable substitution and special escape sequences. We will look at the special escape sequences in this chapter and discuss quoting and variables in Chapter 5, "What's in a Name?"

Perl uses some characters for special purposes, such as the dollar sign ($) and the at (@) sign. If these special characters are to be treated as literal characters, they may be preceded by a backslash (`\`) or enclosed within single quotes ('). Use the backslash to quote a single character rather than a string of characters.
