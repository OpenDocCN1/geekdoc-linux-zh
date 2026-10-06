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