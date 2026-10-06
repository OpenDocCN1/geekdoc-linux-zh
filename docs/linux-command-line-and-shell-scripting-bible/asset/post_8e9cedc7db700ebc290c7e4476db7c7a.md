
The quick brown fox jumps over the lazy dog
The quick brown fox jumps over the lazy dog
The quick brown fox jumps over the lazy dog
$ sed 'd' data1

The delete command is obviously most useful when used in conjunction with a specific address.
This allows you to delete specific lines of text from the data stream, either by line number:

```
$ sed '3d' data6
This is line number 1.
This is line number 2.
This is line number 4.
$
```

or by a specific range of lines:

```
$ sed '2,3d' data6
This is line number 1.
This is line number 4.
$
```

or by using the special end of file character:

```
$ sed '3,$d' data6
This is line number 1.
This is line number 2.
$
```

The pattern-matching feature of the sed editor also applies to the delete command:

```
$ sed '/number 1/d' data6
This is line number 2.
This is line number 3.
This is line number 4
$
```

The sed editor removes the line containing text that matches the pattern you specify.

> NOTE Remember that the sed editor doesn't touch the original file. Any lines you delete are only gone from the output of the sed editor. The original file still contains the 'deleted' lines.

You can also define a range of lines using two text patterns, but be careful if you do this. The first pattern 'turns on' the line deletion, and the second pattern 'turns off' the line deletion. The sed editor deletes any lines between the two specified lines (including the specified lines):

```
$ sed '/1/,/3d' data6
This is line number 4.
$
```

# Part III Advanced Shell Scripting

I mentioned that you need to be careful with this, as the delete feature will “turn on” whenever the sed editor detects the start pattern in the data stream. This may produce an unexpected result:

```
$ cat data7
This is line number 1.
This is line number 2.
This is line number 3.
This is line number 4.
This is line number 1 again.
This is text you want to keep.
This is the last line in the file.
$ sed '/1/./3/d' data7
This is line number 4.
$
```

The second occurrence of a line with the number 1 in the data stream, it triggered the delete command again, deleting the rest of the lines as the stop pattern wasn’t recognized. Of course, the other obvious problem occurs if you specify a pattern that never appears in the text:

```
$ sed '/1/./5/d' data7
```

Since the delete features “turned on” at the first pattern match, but never found the end pattern match, the entire data stream. The difference between the two actions can be confusing:

# Inserting and appending text

As you would expect, like any other editor, the sed editor allows you to insert and append text lines to the data stream. The difference between the two actions can be confusing:

- The insert command (i) adds a new line before the specified line
- The append command (a) adds a new line after the specified line

A confusing about these two commands is their formats. You can’t use these commands on a single line. You must specify the line to insert or append on a separate line by itself. The format for doing this is:

```
$ sed '[address]command\
new line
```

The text in new line appears in the sed editor output in the place you specify. Remember, when you use the insert command, the text appears in the data stream:

```
$ echo 'testing' | sed 'i\n> This is a test'
This is a test
testing
```

436

# Introducing sed and gawk

And when you use the append command, the text appears after the data stream text:

```
$ echo "testing" | sed 'a\n> This is a test'
testing
This is a test
$
```

When you use the sed editor from the command line interface prompt, you'll get the secondary prompt to enter the new line data. You must complete the sed editor command on this line, for once you enter the ending single quotation mark the bash shell will process the command.

This works great for adding text before or after the text in the data stream, but what about adding text inside the data stream?

To insert or append data inside the data stream lines, you must use addressing to tell the sed editor where you want the data to appear. You can only specify a single line address when using these commands. You can match either a numeric line or a text pattern, but you can't use a range of addresses (that makes sense, as you can only insert or append before or after a single line, not a range).

Here's an example of inserting a new line before 3 in the data stream:

```
$ sed '3ia\n> is an inserted line.' data6
This is line number 1.
This is line number 2.
This is an inserted line.
This is line number 3.
This is line number 4.
$
```

Here's an example of appending a new line after 3 in the data stream:

```
$ sed '3a\n> is an inserted line.' data6
This is line number 1.
This is line number 2.
This is line number 3.
This is an inserted line.
This is line number 4.
$
```

This uses the same process as the insert command; if you have a multiline data stream, and you want to append a new line of text to the end of a data stream, just use our new friend the dollar sign, which represents the last line of data:

```
$ sed '$a\n> This is a new line of text.' data6
```

437

# Part III Advanced Shell Scripting

This is line number 1.
This is line number 2.
This is line number 3.
This is line number 4.
This is a new line of text.

The same idea applies if you want to add a new line at the beginning of the data stream.
insert a new line before line number one.

To insert or append more than one line of text, you must use a backslash on each line of new
text until you reach the last line where you want to insert or append text:

```
$ sed 'li|
> This is one line of new text.\n> This is another line of new text.' data6
This is one line of new text.
This is another line of new text.
This is line number 1.
This is line number 2.
This is line number 3.
This is line number 4.
$
```

Both of the specified lines are added to the data stream.

# Changing lines

The change command allows you to change the contents of an entire line. It works the same way as the insert and append commands, in that you must specify the new line separately from the command:

```
$ sed '3c\n> This is a changed line.'
This is line number 1.
This is line number 2.
This is a changed line.
This is line number 4.
$
```

In this example the sed editor changes line number 3. You can also use a text
for the address:

```
$ sed '/number 3/\n> This is a changed line.'
This is line number 1.
This is line number 2.
This is a changed line.
This is line number 4.
$
```

# Introducing sed and awk 16

The text pattern command will change any line of text in the data stream that it matches.

```
$ sed '/number/1c\
> This is a changed line.' data7
This is a changed line.
This is line number 2.
This is line number 3.
This is line number 4.
This is a changed line.
This is yet another line.
This is the last line in the file.
$
```

You can use an address range in the change command, but the results may be what you expect:

```
$ sed '2,3c\
> This is a new line of text.' data6
This is line number 1.
This is a new line of text.
This is line number 4.
$
```

Instead of changing both lines with the text, the sed editor uses the single line of text to replace both lines.

# The transform command

The transform command (y) is the only sed editor command that operates on a single character. The transform command uses the format:

```
[address]/inchars/outchars/
```

The transform command performs a one-to-one mapping of the inchars and the outchars values. The first character in inchars is converted to the first character in outchars. The second character in inchars is converted to the second character in outchars. This mapping continues throughout the length of the specified characters. If the inchars and outchars are not the same length, the sed editor will produce an error message.

A simple example of using the transform command is:

```
$ sed 'y/123/789/'
This is line number 7.
This is line number 8.
This is line number 9.
This is line number 4.
This is line number 7 again.
This is yet another line.
This is the last line in the file.
$
```

439
