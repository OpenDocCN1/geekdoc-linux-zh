# Copy Files: cp

The cp command is used to copy files. It has a substantial number of options. See its man page for additional details. By default, this command works silently, displaying status information only if an error condition occurs. Following are the most common options for cp:

| Option | Description |
| -f | Forces copy; does not ask for verification |
| -i | Interactive copy; before each file is copied, verifies with user |
| -R, -r | Copies directories recursively |

First, let's use the touch command to create an empty file called foo.txt in the user's home directory:

```
master@server ~$ touch foo.txt
```

Then use the cp (copy) command to copy foo.txt to foo.txt.html:

```
master@server ~$ cp foo.txt foo.txt.html
```

To copy all files in the current directory ending in .html to the /tmp directory, type this:

```
master@server ~$ cp *.html /tmp
```

To iteratively recopy all files in the current directory ending in .html to the /tmp directory, type this command:

```
master@server ~$ cp -i *.html /tmp
cp: overwrite /tmp/foo.txt.html? yes
```

You will notice that using the interactive (-i) option with cp forces it to prompt or warn you before overwriting existing files with the same name in the destination. To continue the copy and overwrite the existing file at the destination, type yes or y at the prompt like this:

```
master@server ~$ cp -i *.html /tmp
cp: overwrite /tmp/foo.txt.html? yes
```

# Move Files: mv

The mv command is used to move files from one location to another. Files can be moved across partitions/file systems as well. Moving files across partitions involves a copy operation, and as a result, the move command can take longer. But you will find that moving files within the same file system is almost instantaneous.