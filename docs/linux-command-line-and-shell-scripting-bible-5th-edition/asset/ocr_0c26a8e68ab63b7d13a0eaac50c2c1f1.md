# Part III: Advanced Shell Scripting

Fortunately, the designers behind the sed editor thought of that situation and devised a solution. The sed editor includes three special commands that you can use to process multiline text:

+   - N adds the next line in the data stream to create a multiline group for processing.
+   - D deletes a single line in a multiline group.
+   - P prints a single line in a multiline group.

The following sections examine these multiline commands more closely and demonstrate how you can use them in your scripts.

# Navigating the next command

Before you can examine the multiline next (N) command, you first need to look at how the single-line version of the next command works. After that, it's much easier to understand how the multiline version of the next command operates.

# Using the single-line next command

The single-line next (n) command tells the sed editor to move to the next line of text in the data stream, without going back to the beginning of the commands. Remember that normally the sed editor processes all the defined commands on a line before moving to the next line of text in the data stream. The single-line next (n) command alters this flow.

This may sound somewhat complicated, and sometimes it is. In this example, a data file contains five lines, two of which are blank. The goal is to remove the first blank line, which is after the header line, but leave the second blank line intact. If you write a sed script to delete blank lines, both blank lines are removed, which is not what you wanted:

```
```bash
$ cat data1.txt
Header Line

Data Line #1

End of Data Lines
$
$ sed 1/^$/d' data1.txt
Header Line
Data Line #1
End of Data Lines
$```
```

Because the line you want to remove is blank, there is no text you can search for to uniquely identify the line. The solution is to use the single-line next (n) command. In this next example, the script looks for a unique line that contains the word Header. After the script identifies that line, the n command moves the sed editor to the next line of text, which is the blank line.