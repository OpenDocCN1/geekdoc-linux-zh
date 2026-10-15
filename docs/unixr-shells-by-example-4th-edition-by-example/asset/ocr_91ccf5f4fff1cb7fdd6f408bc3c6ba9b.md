# 7.7 Quoting

The Bourne shell does not let you know if you have mismatched quotes. If running interactively, a secondary prompt appears when quotes are not matched. If in a shell script, the file is scanned and if the quote is not matched, the shell will attempt to match it with the next available quote; if the shell cannot match it with the next available quote, the program aborts and the message 'end of file' unexpected appears on the terminal. Quoting can be a real hassle for even the best of shell programmers! See “What You Should Know About Quotes” on page 985 for shell quoting rules.

# 7.7.1 The Backslash

The backslash is used to quote (or escape) a single character from interpretation. The backslash is not interpreted if placed in single quotes. The backslash will protect the dollar sign ($), backquotes (`), and the backslash from interpretation if enclosed in double quotes.

# EXAMPLE 7.31

```
1  $ echo Where are you going?\
where are you going?
2  $ echo Start on this line and \
> go to the next line.
Start on this line and go to the next line.
3  $ echo \\
\
4  $ echo '\'
\\
5  $ echo '\$5.00'
\$5.00
6  $ echo "\$5.00"
$5.00
```

# EXPLANATION

+   1 The backslash prevents the shell from performing filename substitution on the question mark.
+   2 The backslash escapes the newline, allowing the next line to become part of this line.
+   3 Because the backslash itself is a special character, it prevents the backslash following it from interpretation.
+   4 The backslash is not interpreted when enclosed in single quotes.
+   5 All characters in single quotes are treated literally. The backslash does not serve any purpose here.
+   6 When enclosed in double quotes, the backslash prevents the dollar sign from being interpreted for variable substitution.