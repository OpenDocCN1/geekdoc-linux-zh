# EXPLANATION (CONTINUED)

+   2 The quotes create a single string. The shell evaluates the string as a single word and the whitespace is preserved.
+   3 This is the raw option. Any escape sequences, such as \r, are not interpreted.
+   4 The -s option appends the print command's arguments to the history file as a command. The string "date +%H" is the argument to the print command. The date string is appended to the history list as a command and then executed with the r command (history's redo command).
+   5 The -n option suppresses the newline. The Korn shell prompt is on the same line as the output from the print command.
+   6 The local variable is assigned the value world. The braces insulate the variable from characters appended to it.
+   7 When the first argument to the print function begins with a dash, the print command interprets the argument as one of its options, unless an additional preceding dash is provided.
+   8 The dash as an option allows you to use a dash as the first character in the string to be printed.

# 11.9.6 Escape Sequences

Escape sequences consist of a character preceded by a backslash and have a special meaning when enclosed within quotes. (See Table 11.11.)

The print command, without the -r and -R options, formats output when any of the following escape sequences are placed within a string. The string must be enclosed in double or single quotes.

# EXAMPLE 11.41

```
1 $ print '\t\t\tHello\n'
    Hello

2 $ print "\aTea \tTime!\n\n"
Ding ( bell rings ) Tea    Time!
```

# EXPLANATION

+   1 The backslash characters must be quoted with either single or double quotes. The \t escape sequence represents a tab, and \n represents a newline. The output is three tabs, followed by the string Hello, and a newline.
+   2 The \a escape sequence causes a bell to ring (\007) and the \t creates a tab. The two \n sequences will print two newline characters.