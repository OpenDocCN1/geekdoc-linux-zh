# EXAMPLE 7.3

```
1  $ PS1="`uname -n` > "
2  chargers >
```

# EXPLANATION

+   1  The default primary prompt is a dollar sign ($). The PS1 prompt is being reset to the name of the machine (`uname -n`) and a > symbol. (Don't confuse backquotes and single quotes.)
+   2  The new prompt is displayed.

The Secondary Prompt. The PS2 prompt is the secondary prompt. Its value is displayed to standard error, which is the screen by default. This prompt appears when you have not completed a command and have pressed the carriage return.

# EXAMPLE 7.4

```
1  $ echo "Hello
2  > there"
3  Hello
    there
4  $

5  $ PS2=">---> "
6  $ echo 'Hi
7  ----->
    -----> there'
    Hi
    there
    $
```

# EXPLANATION

+   1  The double quotes must be matched after the string "Hello.
+   2  When a newline is entered, the secondary prompt appears. Until the closing double quotes are entered, the secondary prompt will be displayed.
+   3  The output of the echo command is displayed.
+   4  The primary prompt is displayed.
+   5  The secondary prompt is reset.
+   6  The single quote must be matched after the string 'Hi.
+   7  When a newline is entered, the new secondary prompt appears. Until the closing single quote is entered, the secondary prompt will be displayed.