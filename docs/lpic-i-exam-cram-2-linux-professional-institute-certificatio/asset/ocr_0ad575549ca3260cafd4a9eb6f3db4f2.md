The reason for the double quotation marks is the space between set and number; otherwise, it would give you a syntax error.

More than 60 options are available in the vi editor. You can view them easily by typing :set all in the editor, or to see which options are currently set for your session, type :set while in the editor. Finally, you can type :set optionname? to find out about that particular option’s status.

For some reason, LPI really wants you to know the options for setting numbers, including the shortcuts for how often you see. Examples of how you could set the numbers option on and off include

+   - :set number—Turns on line numbers (screen only).
+   - :set number—Turns the number option off.
+   - :se nu—This is the shortest string that turns this option on, and putting no in front of the option turns that option off.

# # Advanced vi

Several tasks are part of vi that don’t fit in any other section. Most of these are quite advanced, such as running external commands, joining lines, and splitting windows. This section covers these in detail.

# ## Running External Commands in vi

A frequent question on the exams is how to run an external command inside vi, such as seeing an ls -1 listing of the current directory so you can remember a filename:

```
: ! ls -1
```

In this, the command ls -1 executes, with the command’s output displaying onscreen, and you need only press Enter or enter a command to return to the vi session. If the output scrolls more than one screen, it’s piped to the more command and all the normal movement keystrokes will apply.

# ## Joining Lines

It’s quite irritating in vi to be at the front of a line and want to use the Backspace key to move that line to the end of the previous line. The Backspace key works only on the current line. If you need a line to be joined to the previous line, you can position the cursor in either line and press Shift+J to cause the second to be appended to the end of the first line.