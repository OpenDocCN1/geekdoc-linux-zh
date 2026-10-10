```
```
.: 
bob/        jane/         joe/        lost+found/ mary/          thad/
```
```

Yes, this is the home partition. Now change the current directory to Joe’s home directory using the cd command. Type ls again to view the contents of his home directory.

```
```
restore > cd joe
restore > ls
./joe:
.mozilla/          Desktop/         report.html
.tcshrc            Mail/          letter.txt
.xinitrc           News/          www/
```
```

Now mark the Mail directory for extraction using the add command:

```
```
restore > add Mail
```
```

If you use the ls command again, you see that the Mail directory is preceded with an asterisk (*) character, which means it has been marked for extraction.

```
```
restore > ls
./joe:
.mozilla/          Desktop/         report.html
.tcshrc            *Mail/          letter.txt
.xinitrc           News/          www/
```
```

Now use the extract command to begin the extraction process. restore will prompt you for the number of the tape to start with. This is a single tape backup, so just enter the number 1. When it prompts you to set owner/mode for '.,?' answer yes by typing y and pressing Enter. restore will then restore the file permissions (if necessary) of the directory it is restoring to. This isn’t critical when extracting individual files like this, but you should always answer yes to this prompt when doing a full restore. Anyway, your screen should now contain the following:

```
```
restore > extract
You have not read any tapes yet.
Unless you know which volume your file(s) are on
you should start with the last volume and work toward the first.
Specify next volume #: 1
Set owner/mode for '.,?' [yn] y
restore >
```
```

At this point, the files have been recovered and you can exit the restore program by issuing the quit command. That’s all there is to it. You now know the basics of using the dump and restore commands.