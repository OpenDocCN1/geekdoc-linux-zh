```
Line3
Line4
Line5
Line6
Line7
Line8
Line9
Line10
Line11
Line12
Line13
Line14
Line15
$
$ sed '{
> :start
> $q ; N ; 11,$D
> b start
> }' data7.txt
Line6
Line7
Line8
Line9
Line10
Line11
Line12
Line13
Line14
Line15
$
```

The script first checks whether the line is the last line in the data stream. If it is, the quit (q) command stops the loop. The N command appends the next line to the current line in the pattern space. The $11, $D command deletes the first line in the pattern space if the current line is after line 10. This creates the sliding window effect in the pattern space. Thus, the sed program script displays only the last 10 lines of the data7.txt file.

# Deleting lines

Another useful utility for the sed editor is to remove unwanted blank lines in a data stream. It’s easy to remove all the blank lines from a data stream, but it takes a little ingenuity to selectively remove blank lines. This section shows you three quick sed editor scripts that you