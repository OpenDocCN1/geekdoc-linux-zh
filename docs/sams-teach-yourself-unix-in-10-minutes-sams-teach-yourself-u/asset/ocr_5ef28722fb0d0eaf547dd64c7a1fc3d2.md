For example, issue the command

```
> cp -r /usr/local/httpd/logs /tmp
```

The cp command creates a new directory named logs in the directory /tmp, and makes a copy of the contents of the directory /usr/local/httpd/logs in this new /tmp/logs directory.

# MOVING FILES AND DIRECTORIES: mv

If you simply need to move (rename) files rather than copying them, you want to use the mv command. This command uses the same two forms that the cp command does: The first moves (renames) a file from one name to another name, and the second moves one or more files to a destination directory.

Follow these steps to use the mv command to rename a single file:

+   1. Determine the current name of the file and the name you'd prefer it to have.
+   2. Issue the mv command as: mv <currentname> <newname>.

For example, if you have a file named todays_mail and want to store it away with your backed up email, you might type

```
> mv todays_mail ~/mymaildir/June10.mail
```

This command would move the file todays_mail in the current directory to the file June10.mail located in the directory ~/mymaildir (remember, that's the directory mymaildir located in your home directory).

Follow these steps to use the mv command to move one or more files to a new location:

+   1. Determine the names of all the files you want to move and the name of the directory to which you'd like to move them.
+   2. Issue the mv command as mv <file1> <file2> ... <destinationdir>.

For example

```
> mv /usr/local/httpd/logs/error_log /priv/home/henry/myfile2
/tmp
```