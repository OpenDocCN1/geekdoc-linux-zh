This time the example instructed sed to process only lines situated between <para> and </para>. The instruction used resembles some sort of loop, activated only if the string <para> is found and deactivated again if the string </para> appears. The Tab character was input with Ctrl-V and Tab, as usual. The same result could be achieved with an XSLT stylesheet, but the header alone you would need to use in that stylesheet would be longer than the sed command used.

# A.3.3 Inserting Characters at the Beginning of a Line

If you want to insert characters at the beginning of a line, then you need to “replace” the beginning of the line with the desired characters, as shown in Listing A.12.

# LISTING A.12 Inserting Characters at the Beginning of the Line

```
erikk@unixhost> cat leadwhite2.txt
This is line 1.
This is line 2.
This is line 3.

erikk@unixhost> sed 's/^/xxxxx/' leadwhite2.txt
xxxxxThis is line 1.
xxxxxThis is line 2.
xxxxxThis is line 3.
```

The string “xxxxx” can be replaced by blanks or Tab characters as needed, obviously.

# A.4 THE VI EDITOR

The vi editor is a powerful program, but it is rarely used to its full potential because of the lack of a user interface.

# A.4.1 Cursor Movement

If you need to move the cursor inside a file you opened previously with vi, then you could use the cursor keys. The downside here is as follows: the size of the largest document to be edited with vi is limited only by the available space in the /tmp directory. This means going from line 1 to line 4078 will take a considerable time if the movement is done by using the cursor keys.

You could use the G command in vi’s command mode to speed things up a little. If you use 4078G in command mode, vi will jump to line 4078 from every