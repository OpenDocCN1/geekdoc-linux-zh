
1. To set your current line to line number *n*, enter the following subcommand:

*n*

2. To move the current line forward through the buffer one line at a time press Return.

3. To move the current line backward through the buffer one line at a time, enter a dash (–) character.

4. To move the current line *n* lines forward through the buffer, enter the following subcommand:

.*+n*

5. To move the current line *n* lines backward through the buffer, enter the following subcommand:

.*-n*

## B.4.1 Finding Your Position in the Buffer

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

The $= subcommand is an easy way to find out how many lines are in the buffer. The ed $ symbol has no relationship to the shell prompt ($).

## B.4.2 Changing Your Position in the Buffer

You can change your position in the buffer (change your current line) in one of two ways:

- Specify a line number (an absolute position)
- Move forward or backward relative to your current line

To move the current line to a specific line, enter the line number; ed displays the new current line. In the following example, the first line of a file becomes the current line:

```
1
The only way to stop
```

Pressing Return advances one line through the buffer and displays the new current line, as the following example shows:

```
appending is to enter a

line that contains only

a dot.

?
```

When you try to move beyond the last line of the buffer, ed returns ?, an error message. You cannot move beyond the end of the buffer.

To set the current line to the last line of the buffer, enter $.

To move the current line backward through the buffer one line at a time, enter minus signs (-) one after the other, as the following example shows:

```
- line that contains only
- appending is to enter a
- The only way to stop
- ?_
```

When you try to move beyond the first line in the buffer, you receive the ? message. You cannot move beyond the top of the buffer.

To move the current line forward through the buffer more than one line at a time, enter `.n` (where n is the number of lines you want to move):

```
```text
.2
line that contains only
_
```
```

Note that `.2` is an abbreviation for `.+2`.

To move the current line backward through the buffer more than one line at a time, enter the following subcommand: `-n` (where n is the number of lines you want to move):

```
```text
.-2
The only way to stop
_
```
```

## B.5 Locating Text

If you do not know the number of the line that contains a particular word or another string of characters, you can locate the line with a context search.

To search in context, do one of the following:

- To search forward, enter the following subcommand:

`/string to find/`

- To search backward, enter the following subcommand:

`?string to find?`

The following sections describe these methods of searching text in detail.

### B.5.1 Searching Forward Through the Buffer

To search forward through the buffer, enter the string enclosed in slashes (`/`):

```
```text
/only/
line that contains only
_
```
```

The context search (`/only/`) begins on the first line after the current line, then locates and displays the next line that contains the string "only". That line becomes the current line.

If ed does not find the string between the first line of the search and the last line of the buffer, then it continues the search at line 1 and searches to the current line. If ed searches the entire buffer without finding the string, it displays the `?` error message:
