# ### Using vi

The vi editor is a full-screen text editor, so you can view several lines at the same time. Most UNIX systems, including Linux, come with vi. Therefore, if you know the basic features of vi, you can edit text files on almost any UNIX system.

![](bbox=[0.11, 0.245, 0.18, 0.3])

When vi edits a file, it reads the file into a buffer — a block of memory — so you can change the text in the buffer. The vi editor also uses temporary files during editing, but the original file isn't altered until you save the changes.

To start the editor, type vi and follow it with the name of the file you want to edit, like this:

```
vi /etc/fstab
```

The vi editor then loads the file into memory and displays the first few lines in a text screen and positions the cursor on the first line, as shown in Figure 5-2.

![](bbox=[0.23, 0.47, 0.7, 0.71])

**Figure 5-2:**
You can edit text files with the vi full-screen text editor.

The last line shows the pathname of the file as well as the number of lines (11) and the number of characters (878) in the file. In this case, the text [readonly] appears after the filename because I'm opening the /etc/ fstab file while I'm logged in as a normal user (which means I don't have permission to modify the file). Later, the last line in the vi display functions as a command entry area. The rest of the lines display the file. If the file con- tains fewer lines than the screen, vi displays the empty lines with a tilde (~) in the first column.