This changes the ownership of the /www/myclient directory along with all of its subdirectories and files to myclient (user) and httpd (group). This is done to allow the client user to own, modify, and delete her files and to allow the Web server to read the files in the directory. However, to disallow everyone else, you must change the permissions as follows:

```
chmod -R 2770 /www/client dir
```

For the current example, the actual command is as follows:

```
chmod -R 2770 /www/myclient
```

This sets all the files and subdirectory permissions for /www/myclient to 2770, which allows the files and directories to be readable, writable, and executable by the owner (myclient) and the Web server user (httpd) and also makes sure that when new files are created, they have their permissions set to allow the Web server to read the file. This is done using the set-GID (2) digit.

# Using Common File/Directory Utilities

This section shows you how to work with a few commonly used file and directory utility programs that are readily available on your Red Hat Linux system.

# Viewing files and directories

The ls program probably is the most widely used program on any UNIX or UNIX-like platform. The most widely used options for ls are -l (long listing), -a (all files including filenames starting with a period), -1 (single-column, filenames-only listing), and -R (recursive listing).

# Navigating your way into directories

You likely already know the cd command, which is really a built-in shell command. If you don't provide a directory name as an argument, the cd command returns you to the home directory of the user account you are