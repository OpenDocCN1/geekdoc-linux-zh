# # Remove Directory: rmdir

The rmdir command offers no surprises for those familiar with the DOS version of the command; simply removes an existing directory. This command also accepts the **-p** parameter, which removes parent directories as well.

For example, to remove a directory called mydir, you'd type this:

```
[master@server ~] rmdir mydir
```

If you want to get rid of all the directories from bigdir to finaldir that were created earlier, you'd use this command:

```
[master@server ~] rmdir -p bigdir/subdir/finaldir
```

> > TIP You can also use the rm command with the -r option to delete directories well as any subdirectories.

# # Show Present Working Directory: pwd

Invitably, you will find yourself at the terminal or shell prompt of an already logged-in workstation and won't know where you are in the file system hierarchy or tree. To get information, use the **pwd** command. Its only task is to print the current working directory. To display your current working directory, use this:

```
[master@server ~] pwd
/home/master
```

# # Tape Archive: tar

If you are familiar with the PKZip program, you are accustomed to the fact that the compression tool not only reduces file size but also consolidates files into archives. Under Linux, this is separated into two tools: **gzip** and **tar**.

The tar command combines multiple files into a single large file. It is separate from the compression tool, so it allows you to select which compression tool to use or whether you want compression. In addition, tar is able to read and write to devices, making it a good tool for backing up to tape devices.

> ### The History of tar
Although the tape archive, or tar, program, includes the word "tape," it isn't necessary to read or write to a tape drive when you are creating archives. In fact, you'll rarely use tar with a tape in day-to-day situations any longer (traditional backups aside).
When the program was originally created, limited disk space meant that tape was the most logical place to put archives. Typically, the **-f** option in tar would be used to specify the tape device file, rather than a traditional UNIX file. You should be aware, however, that you can still tar straight to a device.