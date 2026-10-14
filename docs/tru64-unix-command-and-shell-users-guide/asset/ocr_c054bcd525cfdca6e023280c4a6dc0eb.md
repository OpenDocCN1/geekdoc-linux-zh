+   1. To set your current line to line number *n*, enter the following subcommand:
+   
+   *n*

+   2. To move the current line forward through the buffer one line at a time press Return.

+   3. To move the current line backward through the buffer one line at a time, enter a dash (–) character.

+   4. To move the current line *n* lines forward through the buffer, enter the following subcommand:
+   
+   .*+n*

+   5. To move the current line *n* lines backward through the buffer, enter the following subcommand:
+   
+   .*-n*

# B.4.1 Finding Your Position in the Buffer

When you first load a file into the buffer, the last line of the file is the current line. As you work with the file, you usually change the current line many times. You can display the current line or its line number at any time.

To display the current line, enter p:

```
p
a dot.
—
```

The p subcommand displays the current line (a dot.). Because the current line has not been changed since you read a file into the buffer, the current line is the last line of the buffer.

Enter . = to display the line number of the current line:

```
.
=
4
—
```

Since a file has four lines, and the current line is the last line in the buffer, the . = subcommand displays 4.

You also can use the dollar sign (the symbol that stands for the last line in the buffer) with the = subcommand to determine the number of the last line in the buffer:

```
$=
4
```