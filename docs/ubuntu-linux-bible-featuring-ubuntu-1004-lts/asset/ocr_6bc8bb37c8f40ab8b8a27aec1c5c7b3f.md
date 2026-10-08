# Chapter 11: Using Command-Line Tools

As you can see, much of this output is very similar to that of the cp command. In this example, I first used the df command to demonstrate that my current directory ('~') and the target directory (/tmp) are actually located on different filesystems. You can see the difference in the verbose output of the mv command.

Along copying and moving files and directories, deleting files and directories is a common operation. Whether you are deleting things to free up disk space for future projects, deleting backup copies of projects that you've finished, or deleting things that you don't want anyone else to see, it's quite easy to delete files from the command line. The key to doing so is the rm command, which continues the "the less typing, the better" philosophy and stands for remove.

To remove a single file on a Linux system, simply type the rm command followed by the name of the file. For example, to delete the file .txt, you would do the following:

```
$ rm file.txt
```

The file is gone. As with the cp command, the rm command provides an -r (recursive) option to enable you to remove entire directories. For example, to permanently remove a directory named, you would issue the following command:

```
$ rm -r test
```

# Tip

You can remove directories using the rm command, but I don't find that to be a common scenario. I rarely have empty directories sitting around because I usually create directories to store something in them. I generally use the rm command to delete any directory because that way I don't have to delete its contents first. My mileage may vary.

If you moved to Ubuntu from a Microsoft Windows system, you may be aware that it is easy to recover files that you've deleted on a Windows system it initially erases the directory entry that identifies the file or folder you're deleting. This is not the case on a Linux system. When you delete a file or directory on a Linux system using the command line or emptying the Trash in a graphical environment, all of the disk storage associated with the file, directory, and the contents of that directory are returned to a general list of free space that is available on your system. Although deleted files and directories can still be recovered on a Linux system, it is much harder to do so and requires the assistance of someone who really knows the details of the filesystem.

The downside of this is that you can't easily recover any files you've deleted by mistake unless you do so using a graphical utility such as a file manager. To protect yourself from accidentally deleting files, see the section later in this chapter on "Defining and Using Aliases" for information about how to permanently set a safe version of the rm command that will ask you for confirmation before it removes anything.

# Tip

All of the cp, mv, and rm commands have more options than I've covered here. To see all of the options available for any of these commands, use the man or info commands to see the online reference information for the command you're interested in.