# NAVIGATING THE FILE SYSTEM

The most basic commands for dealing with the UNIX file system are the ones for moving between directories and finding out what files are in them. Before moving between them though, it’s a good idea to know where you are.

# WHERE ARE YOU? pwd

The pwd (present working directory) command asks your machine to tell you what directory you’re currently in. Any time you’re running a command line, it’s somewhere in the file system—type pwd and it tells you where.

For example:

```
> pwd
/priv/home/ray/public_html/
```

Path Particulars /priv/home/ray/public_html/ is a path. The simplest explanation of a path is the shortest set of directories through which you must travel from the root directory to get to the current file or directory. Each directory in the path is separated by a /.

# THE HOME DIRECTORY

To each user, one particular directory is special. This is your home directory. From the standpoint of navigating around the file system, this directory is identical to any other; however, it is significant in that when you log on, it is where you will initially be. You can expect that anything in or below your home directory belongs only to you. To make your life easier, UNIX doesn’t require you to remember the path to your home directory. Instead, it allows you to refer to your home directory simply as ~, and to anybody else’s home directory as ~username.

Now that you know where you are, the next thing you might want to know is what files are with you.