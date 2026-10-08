command to change the modification date and make it appear as if it had been modified, thus making it appear to have been modified at the time you touched it. This can be useful when you work with backups in particular, and you may also find other uses for it in your work with Unix.

> Where Did That New File Come From? When “touch” a file by accident, you may wind up with a new file you may not have wanted. If you use the touch command and do not specify the actual file-name (a file that really exists on your system), Unix will create a new file for you. For example, if you said you wanted to touch a file on your system unixmaster, and it was really called unixmasters, then a unixmaster file will be created by Unix within the current directory you are working (or saving). You can do this by typing pwd.

Now that you understand the touch command, let's take a look at how you can use it. In this example we will look at both how to change the modification date of a file and how to make a new file altogether.

+   1. Determine the filename of the file or files you want to update or create.
2. Issue the touch command as touch <filename>.

For example, type

```
> touchfile
```

If the backup file previously existed, its last-modified date would now be set to the current time. If the backup file did not previously exist, it would now exist as an empty file with a last-modification date of the current time. It’s easy.

There are additional uses for the touch command. When you become comfortable enough with Unix to start automating your work using shell