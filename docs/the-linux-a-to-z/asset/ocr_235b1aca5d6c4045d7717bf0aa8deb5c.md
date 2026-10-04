# 3.3.2 File Manipulation

The next set of colon commands to look at allow you to write and read blocks of text to and from files:

+   - `:w` write editor contents to original file;
- `:wq` write file and quit editor (same as ZZ);
- `:w file` write editor contents to named file;
- `:r file` read file into editor after cursor line;
- `:e file` edit a new file replacing old contents;
- `:f file` change the name of the current text to file;
- `:f` print the name and status of the current text.

The :w command writes the text you are editing back to the file whose name you specified when you first entered vi. This command doesn't exit from the editor but leaves you in edit mode after the file write takes place. This is a command you should use from time to time to save any changes you have made so far. The :wq command just combines the effect of :w followed by :q.

Sometimes you may want to modify the contents of a file, but then write the changed version back to a new file, leaving the original file unchanged. This is done with :w file. Another variation on the this command allows you to specify a comma-separated range of line numbers before it. This just writes the appropriately numbered lines to the specified file:

```
:a,bw file  write lines a to b inclusive into file
```

The :r command is used to insert the contents of a specified file into the current text after the current cursor line. This can be useful for building new files up from previously prepared pieces.

When you finish with the current text, if you want to edit another file without having to exit vi and re-enter it, you use the :e file command. At any time during the editing of a file you can change the name that vi will use for the file by default. This is done with the :f file command. If you omit the file name after this command then vi will list the current name it is using for the text along with some status information including the number of lines in the text and the line number of the current cursor line.

# 3.3.3 Line Numbers

All the lines in the text being edited have a line number associated with them. You can move the cursor directly to a particular line with the command:

```
:n  move cursor to line n
```

where n is the number of the line to which you wish to move.