![](bbox=[0.14, 0.11, 0.23, 0.19])

You can delete a directory only when the directory is empty.

To remove an empty directory tree, you can use the -p option, like this:

```
rmdir -p /usr/src/book/java/examples/applets
```

This command removes the empty parent directories of applets. The command stops when it encounters a directory that's not empty.

# Commands for finding files

The find command is very useful for locating files (and directories) that meet your search criteria.

When I began using UNIX many years ago (Berkeley UNIX in the early 1980s), I was confounded by the find command. I stayed with one basic syntax of find for a long time before graduating to more complex forms. The basic syntax that I discovered first was for finding a file anywhere in the file system. Here's how it goes: Suppose you want to find any file or directory with a name that starts with gnome. Type the following find command to find these files:

```
find / -name "gnome*" -print
```

If you're not logged in as root, you may get a bunch of error messages. If these error messages annoy you, just modify the command as follows and the error messages are history. (Or, as UNIX aficionados say, "Send 'em to the bit bucket.")

```
find / -name "gnome*" -print 2> /dev/null
```

This command tells find to start looking at the root directory ( /) to look for filenames that match gnome* and to display the full pathname of any matching file. The last part (2> /dev/null) simply sends the error messages to a special file that's the equivalent of simply ignoring them.

You can use variations of this simple form of find to locate a file in any directory (as well as any subdirectories contained in the directory). If you forget where in your home directory you've stored all files named report* (names that start with report), you can search for the files by using the following command:

```
find ~ -name "report*" -print
```