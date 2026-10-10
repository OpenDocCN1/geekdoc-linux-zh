# ## Part III Administration

As an example, pretend that the user Mike has accidentally deleted his Mail subdirectory from his home directory. Mike happens to be your boss, so it is urgent that you recover his files. Here is how you can go about it.

Load the appropriate tape into the tape drive and log in as root. Use the cd command to go to the top of the /home partition, and then run the restore program in interactive mode:

```
```bash
# cd /home
# restore 1f /dev/nst0
```
```

Verify that you have the backup tape for the /home partition by entering the ls command. You should see something like the following list of directories, representing users who have home directories in /home:

```
```
restore > ls
...
connie/ jessica/ mike/ lost+found/ robert/ timothy/
```
```

Yes, this is the home partition. Now change the current directory to Mike's home directory using the cd command. Type ls again to view the contents of his home directory:

```
```
restore > cd mike
restore > ls
./mike:
.mozilla/ Desktop/ report.html
.tchsrc Mail/ letter.txt
.xinirtc News/ www/
```
```

Now mark the Mail directory for extraction using the add command:

```
```
restore > add Mail
```
```

If you use the ls command again, you see that the Mail directory is preceded with an asterisk (*) character, which means that it has been marked for extraction.

```
```
restore > ls
./mike:
.mozilla/ Desktop/ report.html
.tchsrc *Mail/ letter.txt
.xinirtc News/ www/
```
```

Now use the extract command to begin the extraction process. restore will prompt you for the number of the tape to start with. This is a single-tape backup, so just enter the number 1. When it prompts you to set owner/mode for *, .?, answer yes by typing y and pressing [Enter]; restore will then restore the file permissions (if necessary) of the directory it is restoring to. This isn't critical when extracting individual files like this, but you should always answer yes to this prompt when doing a full restore. Anyway, your screen should now contain the following:

```
```
restore > extract
You have not read any tapes yet.
Unless you know which volume your file(s) are on you
```
```