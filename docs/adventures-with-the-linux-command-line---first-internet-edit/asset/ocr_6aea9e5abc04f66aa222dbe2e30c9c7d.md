Using the browser is easy. To select a file or directory, we can use the up and down arrows (or Ctrl-p and Ctrl-n) to move the cursor. Press Enter will open the selected file or directory.

# :find

:find command loads a file by searching a path variable maintained by vim. :find we can specify a partial file name, and vim will attempt to locate the file and automatically complete the name when Tab key is pressed.

The action of :find command can be enhanced if the characters "***" are appended to the end of the path. The best way to do this is:

```
:set path=**
```

Adding this to the path allows :find to search directories recursively. For example, we could change the current working directory to the top of a project's source file tree and :find to load any file in the entire tree.

# wildmenu

Another cool enhancement we command line can apply is the wildmenu. This is a highlighted bar that will appear above the command line when we are entering file names. The word "wild" in the name refers to use of the "wild" key, by default When the wild key is pressed, automatic completion is attempted with the list of possible matches displayed in the wildmenu. Using the left and right arrow keys (or Ctrl-p and Ctrl-n) allows us to choose one of the displayed items.