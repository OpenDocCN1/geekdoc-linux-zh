```
```
Line one.

Line two.

Line three.

Line four.
```
$ 
```

No matter how many blank lines appear between lines of data in the file, the output places only one blank line between the lines.

# ### Deleting leading blank lines

It is also a nuisance when data files contain multiple blank lines at the start of the file. Often when you are trying to import data from a text file into a database, the blank lines create null entries, throwing off any calculations using the data.

Removing blank lines from the top of a data stream is not a difficult task. Here's the script that accomplishes that function:

```
```
///,$!d
```
```

The script uses an address range to determine what lines are deleted. The range starts with a line that contains a character and continues to the end of the data stream. Any line within this range is not deleted from the output. This means that any lines before the first line that contain a character are deleted.

Look at this simple script in action:

```
```
$ cat data9.txt
```
Line one.

Line two.

Line three.

Line four.

```

```
```
$ sed '///,$!d' data9.txt
```
Line one.

Line two.
```

The test file contains two blank lines before the data lines. The script