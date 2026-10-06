```
$ cat print3_6
3,6 p
```

```
$ sed -n -f print3_6 new
The third.
This is line four.
Five.
This is the sixth sentence.
```

The following sed script, append_demo, demonstrates the Append instruction.
The instruction in the script file selects line 2 and appends a NEWLINE and the text AF-TER. to the selected line. Because the command line does not include the -n option, sed copies all the lines from the input file new:

```
$ cat append_demo
2 a\
AFTER.
```

```
$ sed -f append_demo new
Line one.
The second line.
AFTER.
The third.
This is line four.
Five.
This is the sixth sentence.
This is line seven.
Eighth and last.
```

The insert_demo script selects all the lines containing the string This and inserts a NEWLINE and the text BEFORE. before the selected lines:

```
$ cat insert_demo
/This/ /i\
BEFORE.
```

```
$ sed -f insert_demo new
Line one.
The second line.
The third.
BEFORE.
This is line four.
Five.
BEFORE.
This is the sixth sentence.
BEFORE.
This is line seven.
Eighth and last.
```

The next example demonstrates a Change instruction with an address range.
When you give a Change instruction a range of lines, it does not change each linenwithin the range but changes the block of text to a single occurrence of the new text: