none of the specified characters
asas above
abbreviation for the home directory

When handling directories, the two files (they are actually links) . and .. are very important . refers to the current directory, . to the next one above.

Wildcards are not evaluated by the command in which they occur, but by the shell in which the command is called. In addition to the wildcards described above, bash, the most used shell under Linux, recognizes a lot more special characters that have a special effect when executing a command (see 396).

# Complications using wildcards

On the surface, handling wildcards looks easier than it actually is. If you experience problems with wildcards, you should simply carry out some experiments with wildcards. This command displays all file names included in a wildcard combination, without any further effects on files or file names.

One problem is * not only includes files, but also directories.* not only shows all in the current directory, but also the contents of all subdirectories in *. For the ls command, this problem can be circumvented by specifying the -d option: other commands, however, do not have an option.

If you want to operate on all directories (but not on normal files), the wildcard combination /* does the trick: this includes all * files which contain a reference to themselves as a subdirectory — and this is the case for directories. (Internally, directories are considered a special form of file — thus the quotes.)

```
user$ echo * /
```

The fact that the command but the shell is responsible for the evaluation of wildcards has some advantages, but also drawbacks. With, with a command such as ls -R *, it is impossible to search for *.tex files in subdirectories as well. The -R for the ls command performs a recursive search of subdirectories and can be compared with the /S option of the DOS command DIR.

The reason is quite simple: the shell expands the pattern *.tex for the current directory and passes ls the list of files. If you do not have any directories with the extension .tex, ls has finished — the -R option cannot do anything about it. Recursive search is only possible in directories that have been passed as parameters.

Linux provides the much more flexible find command to search for files. The example below shows a list of all *.tex files in the current and all subordinate directories.

```
user$ find -name "*.tex"
```

The same must be attributed to the failure of the attempt to delete * files in all subdirectories. The command rm -f * fails in spite of the -r option for recursive elaboration of subdirectories. The reason: * is already expanded by