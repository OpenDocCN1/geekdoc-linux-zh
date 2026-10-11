# 4.3 The print Function

# EXPLANATION

The string is enclosed in single quotes. This allows the conversational quotes to be printed as literals. The single quote in `can't` is quoted with a backslash so that it will also be printed literally. If it were not, it would be matched with the first single quote. The ending single quote would then have no mate, and, alas, the program would either tell you that you have a runaway quote or search for its mate until it reached the end of file unexpectedly.

The `qq` construct replaces double quotes. Now parentheses delimit the string. Because the `qq` is used, the dollar sign ($) in $5.00 is interpreted as a scalar variable with a null value. The `.00` is printed. (This is not the way to handle your money!) The single `q` replaces single quotes. The `$5` is treated as a literal. Unfortunately, so is the `\n` because backslash interpretation does not take place within single quotes. Without a newline, the next line is run together with line 4. In the next line, if the dollar sign is preceded by a backslash, the backslash "escapes" the special meaning of the $. Now the string will print correctly.

The `\n` is double quoted with the `qq` construct, the string *I need $5.00* is single quoted with the `q` construct, and old-fashioned double quotes are used for the second `\n`.

An alternative delimiter, the exclamation point (!), is used with the `q` construct (instead of the forward slash) to delimit the string.

The string *The present working directory* is is enclosed in double quotes; the UNIX command `pwd` is enclosed in backquotes for command substitution. The `qq` construct quotes *Today*; the `qx` construct replaces the backquotes used for command substitution. Note: To get the same results for MS-DOS, the date command takes the `/T` option. A different delimiter is used because of the slash in `/T`. Typing `q\date//T` would produce an error, so change the delimiter to something else, in this case a #.

Alternative delimiters, the curly braces, are used with the `qx` construct (instead of the forward slash). The output of the UNIX `date` command is printed.

Quoting rules affect almost everything you do in Perl, especially when printing a string of words. Strings are normally delimited by a matched pair of either double or single quotes. When a string is enclosed in single quotes, all characters are treated as literals. When a string is enclosed in double quotes, however, *almost* all characters are treated as literals, with the exception of those characters that are used for variable substitution and special escape sequences. We will look at the special escape sequences in this chapter and discuss quoting and variables in Chapter 5, "What's in a Name?"

Perl uses some characters for special purposes, such as the dollar sign ($) and the at (@) sign. If these special characters are to be treated as literal characters, they may be preceded by a backslash (`\`) or enclosed within single quotes ('). Use the backslash to quote a single character rather than a string of characters.