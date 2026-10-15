Here n is the number of window displays to scroll. This is like pressing PF7 or PF8 n times. If you omit n, the editor scrolls one window backward or forward.

If you enter a BACKWARD subcommand when the current line is the Top of File line, the editor wraps around the file, making the last line of the file the new current line. Similarly, if you enter a FORWARD subcommand when the current line is the End of File line, the editor makes the first line of the file the new current line.

Suppose the file is many screens long and the current screen display is somewhere in the middle of the file. To return to the beginning of the file, you could enter multiple BACKWARD subcommands, or you can enter the TOP subcommand.

The TOP subcommand makes the Top of File line the new current line. Enter the TOP subcommand as shown:

```
====> top
```

The BOTTOM subcommand makes the last line of the file the new current line. Enter the BOTTOM subcommand as shown:

```
====> bottom
```

These subcommands are useful when you want to insert new lines either at the beginning or end of a file.

Suppose that you want to move the file up or down a few lines instead of a whole window. Use the DOWN subcommand to advance the line pointer one or more lines toward the end of a file. The line pointed to becomes the new current line. For example, the following command causes the fifth line down from the current line to be the new current line:

```
====> down 5
```

If you omit the number, then 1 (one line) is assumed. The UP subcommand moves the line pointer toward the beginning of the file. The line pointed to becomes the new current line. For example, the following command causes the fifth line up from the current line to be the new current line.

```
====> up 5
```

Again, if you omit the number, then 1 (one line) is assumed.

z/OS analogy: In z/OS (ISPF editor), these commands are identical.