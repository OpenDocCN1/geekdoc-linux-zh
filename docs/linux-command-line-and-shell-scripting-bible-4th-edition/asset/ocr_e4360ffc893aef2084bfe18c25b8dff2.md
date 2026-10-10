script to delete blank lines, both blank lines are removed, which is not what we wanted:

```
```
$ cat data1.txt
Header Line

Data Line #1

End of Data Lines
$
$ sed '/^$/d' data1.txt
Header Line
Data Line #1
End of Data Lines
$
```
```

Because the line we want to remove is blank, there is no text we can search for to uniquely identify the line. The solution is to use the single-line next (n) command. In this next example, the script looks for a unique line that contains the word Header. After the script identifies that line, the n command moves the sed editor to the next line of text, which is the blank line.

```
```
$ sed '/Header/{n ; d}' data1.txt
Header Line
Data Line #1

End of Data Lines
$
```
```

At that point, the sed editor continues processing the command list, which uses the d command to delete the empty line. When the sed editor reaches the end of the command script, it reads the next line of text from the data stream and starts processing commands from the top of the command script. The sed editor does not find another line with the word Header; thus, no further lines are deleted.

# **Combining lines of text**

Now that you've seen the single-line next (n) command, we can look at the multiline version. The single-line next command moves the next line of text from the data stream into the processing space (called the pattern space) of the sed editor. The multiline version of the next