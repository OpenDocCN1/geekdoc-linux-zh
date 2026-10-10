another, typically complicated, command. You can view all the current aliases your process has by typing `alias` at the command line.

# **Listing 3.3**: Exploring the `ll` command

```
```
$ ls -l
total 32
drwxrwxr-x. 2 Christine Christine     6 Aug 19 17:34 Everything
drwxrwxr-x. 2 Christine Christine     6 Aug 19 17:34 Life
-rw-r--r--. 1 Christine Christine 29900 Aug 19 17:37 Project42.txt
drwxrwxr-x. 2 Christine Christine     6 Aug 19 17:34 Universe
$
$ ll
total 32
drwxrwxr-x. 2 Christine Christine     6 Aug 19 17:34 Everything
drwxrwxr-x. 2 Christine Christine     6 Aug 19 17:34 Life
-rw-r--r--. 1 Christine Christine 29900 Aug 19 17:37 Project42.txt
drwxrwxr-x. 2 Christine Christine     6 Aug 19 17:34 Universe
```

```

If you're working with lots of files and directories, sometimes it helps to see a graphical overview of things. If you don't have access to a graphical desktop, you can still view things on the command line in a pseudo-graphical format using the `tree` command, as shown in Figure 3.1.

![](bbox=[0.15, 0.55, 0.85, 0.9])