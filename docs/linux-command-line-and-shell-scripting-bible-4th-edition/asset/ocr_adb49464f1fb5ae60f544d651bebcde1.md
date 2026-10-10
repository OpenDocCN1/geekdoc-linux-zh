# **Printing last lines**

So far, we've covered how to use the p command to print all the lines in a data stream or just lines that match a specific pattern. What if you just need to work with the last few lines of a long listing, such as a log file?

The dollar sign represents the last line of a data stream, so it's easy to display just the last line:

```
```
$ sed -n '$p' data2.txt
End of Data Lines
$```

```

Now, how can you use the dollar sign symbol to display a set number of lines at the end of the data stream? The answer is to create a *rolling window*.

A rolling window is a common way to examine blocks of text lines in the pattern space by combining them using the n command. The n command appends the next line of text to the text already in the pattern space. After you have a block of 10 text lines in the pattern space, you can check to see if you're at the end of the data stream using the dollar sign. If you're not at the end, continue adding more lines to the pattern space while removing the original lines (remember the d command, which deletes the first line in the pattern space).

By looping through the n and d commands, you add new lines to the block of lines in the pattern space while removing old lines. The branch (b) command is the perfect fit for the loop. To end the loop, just identify the last line and use the q command to quit.

Here's what the final sed editor script looks like:

```
```
$ cat data7.txt
Line1
Line2
Line3
Line4
Line5
Line6
Line7
Line1
Line2
```

```