```
# Find and print the files with inode number
echo "Inks: using find to search for links..." 1&2
find "$directory" -xdev -inum $inode -print
```

The find utility searches for files that meet the criteria specified by its arguments, beginning its search with the directory specified by its first argument ($directory in this case) and searching all subdirectories. The last three arguments specify that the filenames of files having inodes matching $inode should be sent to standard output. Because files in different filesystems can have the same inode number and not be linked, find must search only the directories in the same filesystem as $file for accounts. The -xdev argument to find the search of subdirectories of other filesystems. Refer to page 123 and page 968 for more information about file-systems and links. Refer to page 1165 in Part III for more information on find.

The echo above the find command in Inks, which tells the user that find is running, is included because find frequently takes a long time to run. Because Inks does not include a final statement, the exit status of Inks is that of the last command it runs, find.

# Debugging Shell Scripts

When you are writing a script as Inks, it is easy to make mistakes. While you are debugging a script, you can use the shell's -x option, which causes the shell to display each command before it runs the command. This trace of a script's execution can give you a lot of information about where the problem is.

Suppose Alex wants to run Inks as in the previous example, while displaying each command before it is executed. He can either set the -x option for the current shell (-x) so that all scripts display commands as they are run or use the -x option to affect only the script he is currently executing:

```
$ bash -x Inks letter /home
```

Each command that the script executes is preceded by a plus sign (+) so that you can distinguish the output of the trace from any output that your script produces. You can also set the -x option of the shell running your script by putting the following set command at the top of the script:

```
set -x
```

Turn off the debug option with a plus sign:

```
set +x
```