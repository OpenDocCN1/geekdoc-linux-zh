# Table 13.22 Special Metacharacters Requiring Quotes (continued)

| Metacharacter | Meaning |
|---|---|
| newline | Command termination |
| space/tab | Word delimiter |
| $ | Variable substitution character |
| * [ ] ? | Shell metacharacters for filename expansion |

Single and double quotes must be matched. Single quotes protect special metacharacters, such as $, &, ?, |, >, and <, from interpretation. Double quotes also protect special metacharacters from being interpreted, but allow variable and command substitution characters (the dollar sign and backquotes) to be processed. Single quotes will protect double quotes and double quotes will protect single quotes.

Unlike the Bourne shell, bash tries to let you know if you have mismatched quotes. If running interactively, a secondary prompt appears when quotes are not matched; if in a shell script, the file is scanned and if the quote is not matched, the shell will attempt to match it with the next available quote. If the shell cannot match it with the next available quote, the program aborts and the message bash:unexpected EOF while looking for "" appears on the terminal. Quoting can be a real hassle for even the best of shell programmers!

# 13.11.1 The Backslash

The backslash is used to quote (or escape) a single character from interpretation. The backslash is not interpreted if placed in single quotes. The backslash will protect the dollar sign ($), backquotes (`), and the backslash from interpretation if enclosed in double quotes.

# EXAMPLE 13.72

```
1  $ echo where are you going?\n
   where are you going?
2  $ echo Start on this line and \
>  go to the next line.
   Start on this line and go to the next line.
3  $ echo \\
\
4  $ echo '\'
\\
5  $ echo '\$5.00'
\$5.00
```