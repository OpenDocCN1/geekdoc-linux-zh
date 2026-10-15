So, to find a series of unflattering references to your boss and replace them with "Priscilla," the following will work:

```
1,$s/catbrain/Priscilla/g
```

As a substitute for the 1,$ of this command, you can use % if saving the two keystrokes is important enough to you to bother remembering it.

# Do I have to know what line I'm on to run substitute on the next ten lines?

No. Use the . (dot) to represent the current line, and then tell vi to do the substitution for the next ten lines:

```
.,+10s/fishbreath/Alfie/g
```

To make sure you don't accidentally change something you didn't mean to, use the c option after the final slash. This will print the string to be substituted with "A" characters highlighting it. Press Y to make the change, and anything else to leave it as is.

# How can I execute a command on an entire file?

Use the global command. This lets you search through a file and execute the yank command, for example, to append the lines that match a particular pattern to a buffer. Thus:

```
:g/Priscilla/y A
```

will grab all those lines with "Priscilla" in them, place them in buffer a, appending them after anything that is already there. This command lets you do some fairly tricky things, like search for all lines that begin with a number, and indent them five spaces:

```
:g/^[0-9]/s/^/     /g
```

Using this command, the text in Figure 4-1 becomes lined up like the text in Figure 4-2.