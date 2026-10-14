
| Option | Meaning |
|---|---|
| -v, --verbose | Display informative messages as the move is performed. |

Table 4-7 provides some examples of using the mv command.

Table 4-7: mv Examples

| Command | Results |
|---|---|
| mv file1 file2 | Move file1 to file2. If file2 exists, it is overwritten with the contents of file1. If file2 does not exist, it is created. In either case, file1 ceases to exist. |
| mv -i file1 file2 | Same as the previous command, except that if file2 exists, the user is prompted before it is overwritten. |
| mv file1 file2 dir1 | Move file1 and file2 into directory dir1. The directory dir1 must already exist. |
| mv dir1 dir2 | If directory dir2 does not exist, create directory dir2 and move the contents of directory dir1 into dir2 and delete directory dir1. If directory dir2 does exist, move directory dir1 (and its contents) into directory dir2. |

## rm—Remove Files and Directories

The rm command is used to remove (delete) files and directories, as shown here:

```
rm item...
```

where item is one or more files or directories.

## Useful Options and Examples

Table 4-8 describes some of the common options for rm.

Table 4-8: rm Options

| Option | Meaning |
|---|---|
| `-i, --interactive` | Before deleting an existing file, prompt the user for interactive confirmation. **If this option is not specified, rm will silently delete files.** |
| `-r, --recursive` | Recursively delete directories. This means that if a directory being deleted has subdirectories, delete them too. To delete a directory, this option must be specified. |
| `-f, --force` | Ignore nonexistent files and do not prompt. This overrides the `--interactive` option. |
| `-v, --verbose` | Display informative messages as the deletion is performed. |

> ### BE CAREFUL WITH RM!
> 
> Unix-like operating systems such as Linux do not have an undelete command. Once you delete something with `rm`, it’s gone. Linux assumes you’re smart and you know what you’re doing.
> 
> Be particularly careful with wildcards. Consider this classic example. Let’s say you want to delete just the HTML files in a directory. To do this, you type the following:
> 
> ```bash
> rm *.html
> ```
> 
> This is correct, but if you accidentally place a space between the `*` and the `.html` like so:
> 
> ```bash
> rm * .html
> ```
> 
> The `rm` command will delete all the files in the directory and then complain that there is no file called `.html`.
> 
> Here is a useful tip: whenever you use wildcards with `rm` (besides carefully checking your typing!), test the wildcard first.

with ls. This will let you see the files that will be deleted. Then press the up arrow to recall the command and replace ls with rm.

Table 4-9 provides some examples of using the rm command.

Table 4-9: rm Examples

| Command | Results |
|---|---|
| rm file1 | Delete file1 silently. |
| rm -i file1 | Same as the previous command, except that the user is prompted for confirmation before the deletion is performed. |
| rm -r file1 dir1 | Delete file1 and dir1 and its contents. |
| rm -rf file1 dir1 | Same as the previous command, except that if either file1 or dir1 does not exist, rm will continue silently. |

## ln—Create Links

The ln command is used to create either hard or symbolic links. It is used in one of two ways. The following creates a hard link:

```
ln file link
```

The following creates a symbolic link:

```
ln -s item link
```

where item is either a file or a directory.

## Hard Links

Hard links are the original Unix way of creating links, compared to symbolic links, which are more modern. By default, every file has a single hard link that gives the file its name. When we create a hard link,

we create an additional directory entry for a file. Hard links have two important limitations.

- A hard link cannot reference a file outside its own file system. This means a link cannot reference a file that is not on the same disk partition as the link itself.
- A hard link may not reference a directory.

A hard link is indistinguishable from the file itself. Unlike a symbolic link, when you list a directory containing a hard link, you will see no special indication of the link. When a hard link is deleted, the link is removed, but the contents of the file itself continue to exist (that is, its space is not deallocated) until all links to the file are deleted.

It is important to be aware of hard links because you might encounter them from time to time, but modern practice prefers symbolic links, which we will cover next.

## Symbolic Links

Symbolic links were created to overcome the limitations of hard links. They work by creating a special type of file that contains a text pointer to the referenced file or directory. In this regard, they operate in much the same way as a Windows shortcut, though of course they predate the Windows feature by many years.

A file pointed to by a symbolic link and the symbolic link itself are largely indistinguishable from one another. For example, if you write something to the symbolic link, the referenced file is written to. When you delete a symbolic link, however, only the link is deleted, not the file itself. If the file is deleted before the symbolic link, the link will continue to exist but will point to nothing. In this case, the link is said to be broken. In many implementations, the ls command will display broken links in a distinguishing color, such as red, to reveal their presence.

The concept of links can seem confusing, but hang in there. We’re going to try all this stuff, and it will, ideally, become clear.
