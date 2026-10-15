# EXAMPLE 9.63

```
1 % echo Who are you?
echo: No match.
2 % echo Who are you\?
who are you?
3 % echo This is a very,very long line and this is where \
break the line.
This is a very, very long line and this is where
I break the line.
4 % echo "\\abc
\\|abc
% echo '\abc'
\\|abc
% echo \\abc
\\abc
5 % echo Wow\!
Wow!
```

# EXPLANATION

+   1 The question mark is used for filename expansion. It matches for a single character. The shell is looking for a file in the current directory that is spelled y-o-u, followed by a single character. Because there is not a file by that name in the directory, the shell complains that it could not find a match with No match.
+   2 The shell will not try to interpret the question mark, because it is escaped with the backslash.
+   3 The string is continued to the next line by escaping the newline with a backslash.
+   4 If the backslash is enclosed in either single or double quotes, it is printed. When not enclosed in quotes, the backslash escapes itself.
+   5 The exclamation point must be escaped with a backslash. Otherwise the C shell will perform history substitution.

# 9.12.2 Single Quotes

Single quotes must be matched on the same line and will escape all metacharacters with the exception of the history (bang) character (!). The history character is not protected because the C shell evaluates history before it does quotes, but not before backslashes.

# EXAMPLE 9.64

```
1 % echo 'I need $5.00'
I need $5.00
2 % echo 'I need $500.00 now\!\!'
I need $500.00 now!!
```