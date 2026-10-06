
There's still one subtle problem with this script though. The script always reads the next line of text into the pattern space before executing the sed commands. When it reaches the last line of text, there isn't a line of text to read, so the N command causes the sed editor to stop. If the matching test is on last line in the data stream, the commands won't catch the matching data:

```
$ cat data4
The first meeting of the Linux System
Administrator's group will be held on Tuesday.
All System Administrators should attend this meeting.
$ sed '
> s/System\nAdministrator/Desktop\nUser/
> s/System Administrator/Desktop User/
> data4
The first meeting of the Linux Desktop
User's group will be held on Tuesday.
All System Administrators should attend this meeting.
$
```

Since the System Administrator appears in the last line of the data stream, the N command misses it, as there isn't another line to read into the pattern space to combine. You can easily resolve this by moving your single-line commands before the N command and having only the multiline commands after the N command, like this:

```
$ sed '
> s/System Administrator/Desktop User/
> s/System\nAdministrator/Desktop\nUser/
> data4
The first meeting of the Linux Desktop
User's group will be held on Tuesday.
All Desktop Users should attend this meeting.
$
```

Now, the substitution command that looks for the phrase in a single line works just fine on the last line in the data stream, and the multiline substitution command covers the occurrence in the middle of the data stream.

# The multiline delete command

Chapter 16 introduced the single-line delete command (d). The sed editor uses it to delete the current line in the pattern space. When working with the N command though, you must be careful when using the single-line delete command:

```
$ sed '
> N
```

# Part III Advanced Shell Scripting

```
> /System\nAdministrator/d
> data4
```

The delete command looked for the words System and Administrator in separate lines and then deleted of the lines in the pattern space. This may or may not have been you intended.

The sed editor provides the multiline delete command (D) that only deletes the first line that is in the pattern space. It removes all characters up to and including the newline character:

```
$ sed '
> N
> /System\nAdministrator/D
> data3
```

Administrator's group will be held on Tuesday.
All System Administrators should attend this meeting.

The second line of text that's added to the pattern space remains intact. This comes in handy if you need to remove a line of text that appears before a line that you find a data string in.

Here's an example of removing a blank line that appears before the first line in a data stream:

```
$ cat data5
```

```
This is the header line.
This is a data line.
```

This is the last line.

```
$ sed '/^$/{
> N
> /header/D
> data5
This is the header line.
This is a data line.
```

This is the last line.
```

This sed editor script looks for blank lines and then uses the N command to add the next line of text into the pattern space. If the new pattern space contents contain the word header, the D command removes the first line in the pattern space. Without the combination of the N and D commands it would be impossible to remove the first blank line without removing all other blank lines.

# The multiline print command

By now you're probably catching on to the difference between the single-line and multiline versions of the commands. The multiline print command (P) follows along using the same technique. It prints only the first line in a multiline pattern space. This includes all characters up to the newline character in the pattern space. It's used similarly to the single-line p command to display text when you use the n option to suppress output from the script.

```
$ sed -n '
> /System\nAdministrator/P
> >data3
The first meeting of the Linux System
```

When the multiline matches, the P command prints only the first line in the pattern space.

The power of the multiline P command comes into play when you combine it with the N and D multiline commands.

The D command has a unique feature in that it forces the sed editor to return to the beginning of the script (it doesn't read a new line of text from the data stream). By including the N command in the command script, you can effectively single-step through the pattern space, matching multiple lines together.

Next, by using the P command, you can print the first line, and then using the D command, you can delete the first line and loop back to the beginning of the script. Once you are back at the script's beginning, the N command reads the next line of text and starts the process all over again. This loop continues until you reach the end of the data stream.

# The Hold Space

The pattern space is an active buffer that holds the text examined by the sed editor while it processes commands. However, it isn't the only space available in the sed editor for storing text.

The sed editor utilizes another buffer area called the hold space. You can use the hold space to temporarily hold lines of text while working on other lines in the pattern space. There are five commands associated with operating with the hold space, shown in Table 18-1.

These commands let you copy text from the pattern space to the hold space. This frees up the pattern space to load another string for processing.

# Part III Advanced Shell Scripting

# TABLE 18-1

| Command | Description |
| --- | --- |
| h | Copy pattern space to hold space |
| H | Append pattern space to hold space |
| g | Copy hold space to pattern space |
| G | Append hold space to pattern space |
| x | Exchange contents of pattern and hold space |

Usually, using the h or H commands to move a string to the hold space, eventually you want to use the g, G, or x commands to move the stored string back into the pattern space (otherwise, you wouldn't have cared about saving them in the first place).

With two buffer areas, trying to determine what line of text is in which buffer area can sometimes get confusing. Here's a short example that demonstrates using the h and g commands to move data back and forth between the sed editor buffer spaces:

```
$ cat data2
This is the header line.
This is the first data line.
This is the second data line.
This is the last line.
$ sed -n '/first//
> h
> p
> n
> p
> g
> p
)'
This is the second data line.
This is the first data line.
$
```

Take a look at this example step by step:

- 1. The sed script uses a regular expression in the address to filter the line containing first.
- 2. When the line containing first appears, the h command places the line in the hold space.
- 3. The p command prints the contents of the pattern space, which is still the first line.
- 4. The n command retrieves the next line in the data stream and places it in the pattern space.
- 5. The p command prints the contents of the pattern space, which is now the second data line.
- 6. The g command places the contents of the hold space (the first data line) back in the pattern space, replacing the current text.
- 7. The p command prints the contents of the pattern space, which is now back to the first line.

By shuffling the text lines around the hold space, you are able to force the first data line to appear after the second data line in the output. If you drop the first p command, you can output the two lines in reverse order:

```
$ sed -n '/first//
h
n
np
g
np
)' data2
This is the second data line.
This is the first data line.
$
```

This is the start of something useful. You can use this technique to create a sed script that reverses an entire file of text lists! To do that though, you need to see the negating feature of the sed editor, which is what the next section is all about.

# Negating a Command

Chapter 16 showed that the sed editor applies commands to every text line in the data stream or to lines specifically indicated by either a single address or an address range. You can also configure a command to not apply to a specific address or address range in the data stream.

The exclamation mark (!) is used to negate a command. What this means is that in situations where the command would normally have been activated, it isn't. Here's an example demonstrating this:

```
$ sed -n '/header/lp' data2
This is the first data line.
This is the second data line.
This is the last line.
$
```
