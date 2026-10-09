Here the user `cgi` user owns the directory and the group (specified by `Group` directive) used for Apache server is the group owner of the directory and its files.

Finally, the log directory used in the `CustomLog` and `ErrorLog` directives should only be writable by the `root` user. Recommended permission setting for such directory (say `/www/logs`) is as follows:

```
chown -R root.root /www/logs
chmod -R 700 /www/logs
```

> Do not allow anyone (including the Apache user or group) to read, write, or execute files in the log directory specified in `CustomLog` and `ErrorLog` directives.

Always make sure that you take a minimalistic approach to allowing access to new directories that are accessible via the Web. Also ensure that you do not allow Web visitors to view any directory listings. You can hide your directory listings using the methods discussed later.

# Directory index file

Whenever a user requests access to a directory via the Web, Apache does one of the following:

+   1. Checks whether the directory is accessible. If it is, it continues; otherwise, it displays an error message.
+   2. After it has determined that the directory is accessible, it looks for the directory index file specified by using the `DirectoryIndex` directive. By default, this file is `index.html`. If it can read this file in the requested directory, the contents of the file are displayed. In the event that such a file does not exist, Apache checks whether it can create a dynamic listing for the directory. If it is allowed to create a dynamic listing, it creates it and displays the contents of the directory to the user.

Because an Apache-created dynamically generated directory listing provides potential bad guys with clues about your directory structure, you should not allow such listings. The simplest way to avoid creating a dynamic directory listing is to create a file with the filename specified in `DirectoryIndex` directive. For example, if you set `DirectoryIndex` as follows:

```
DirectoryIndex index.html index.htm
```

Apache will first look for `index.html` in the requested directory of the URL, and then it will look for `index.htm` if `index.html` is missing.

However, a common reasons why many Web sites have exposed directories is that when the new directory is created, the creator forgets to create the index file or uploads an index file with the wrong case, such as `INDEX.HTML` or `INDEX.HTM`.