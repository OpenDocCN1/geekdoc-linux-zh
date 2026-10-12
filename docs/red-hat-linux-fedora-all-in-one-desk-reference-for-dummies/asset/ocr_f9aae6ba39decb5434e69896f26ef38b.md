# TECHNICAL STUFF

When vi edits a file, it reads the file into a buffer — a block of memory — so you can change the text in the buffer. The vi editor also uses temporary files during editing, but the original file isn't altered until you save the changes.

To start the editor, type vi and follow it with the name of the file you want to edit, like this:

```
vi /etc/fstab
```

The vi editor then loads the file into memory and displays the first few lines in a text screen and positions the cursor on the first line (Figure 6-2).

![](bbox=[0.22, 0.52, 0.78, 0.85])

Figure 6-2:
You can edit text files with the vi full-screen text editor.

The last line shows the pathname of the file as well as the number of lines (8) and the number of characters (621) in the file. In this case, the text [read only] appears after the filename because I'm opening the /etc/fstab file while I am logged in as a normal user (which means I don't have permission to modify the file). Later, the last line in the vi display functions as a command-entry area. The rest of the lines display the file. If the file contains fewer lines than the screen, vi displays the empty lines with a tilde (~) in the first column.

The current line is marked by the cursor, which appears as a small black rectangle. The cursor appears on top of a character.