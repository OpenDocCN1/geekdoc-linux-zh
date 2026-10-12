# ## Changing File Access Permissions with chmod

What you learned about chmod in Chapter 5 can be greatly extended through one simple parameter: -c. This instructs chmod to print a list of all the changes it made as part of its operation, which means we can capture the output and use it for other purposes. For example:

```
```
[paul@caitlin tmp]$ chmod -c 600 *
mode of `1.txt' changed to 0600 (rw-------)
mode of `2.txt' changed to 0600 (rw-------)
mode of `3.txt' changed to 0600 (rw-------)
[paul@caitlin tmp]$ chmod -c 600 *
[paul@caitlin tmp]$
```
```

There the chmod command is issued with -c, and you can see it has output the result of the operation: Three files were changed to rw------- (read and write by user only). However, when the command is issued again, no output is returned. This is because -c prints only the changes that it made. Files already match the permissions you are setting are left unchanged and therefore are not printed.

There are two other parameters of interest: --reference and -R. The first allows you to specify a file to use as a template for permissions rather than specifying permissions yourself. For example, if you want all files in the current directory to have the same permissions as the file /home/paul/myfile.txt, you would use this:

```
`chmod --reference /home/paul/myfile.txt *`
```

You can use -R to enable recursive operation, which means you can use it to chmod a directory and it will change the permissions of that directory as well as all files and sub-directories under that directory. You could use chmod -R 600 /home to change every file and directory under /home become read/write to their owner.

# ## Copying Files with cp

Like mv, which is covered later, cp is a command that is easily used and mastered. However, two marvelous parameters rarely see much use (which is a shame!) despite their power. These are --parents and -u, the first of which copies the full path of the file into the new directory. The second copies only if the source file is newer than the destination.

Using --parents requires a little explanation, so here is an example. You have a file, /home/paul/desktop/documents/work/notes.txt, and want to copy it to your /home/paul/backup folder. You could just do a normal cp, but that would give you /home/paul/backup/notes.txt, so how would you know where that came from later? If you use --parents, the file is copied to /home/paul/backup/desktop/documents/work/notes.txt.

The -u parameter is perfect for synchronizing two directories because it allows you to run a command like cp -Ru myfiles myotherfiles and have cp recopy only files that have changed. The -R parameter means recursive and allows you to copy directory contents.