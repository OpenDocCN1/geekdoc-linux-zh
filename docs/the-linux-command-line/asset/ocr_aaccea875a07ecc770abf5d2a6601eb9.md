# 18 – Searching For Files

As we have wandered around our Linux system, one thing has become abundantly clear: a typical Linux system has a lot of files! This begs the question, “how do we find things?” We already know that the Linux file system is well organized according to conventions that have been passed down from one generation of Unix-like system to the next, but the sheer number of files can present a daunting problem.

In this chapter, we will look at two tools that are used to find files on a system. These tools are:

+   - `locate` – Find files by name
+   - `find` – Search for files in a directory hierarchy

We will also look at a command that is often used with file search commands to process the resulting list of files:

+   - `xargs` – Build and execute command lines from standard input

In addition, we will introduce a couple of commands to assist us in or exploration:

+   - `touch` – Change file times
+   - `stat` – Display file or file system status

# locate – Find Files The Easy Way

The `locate` program performs a rapid database search of pathnames and outputs every name that matches a given substring. Say, for example, we want to find all the programs with names that begin with “zip.” Since we are looking for programs, we can assume that the directory containing the programs would end with “bin/”. Therefore, we could try to use `locate` this way to find our files:

```
[me@linuxbox ~]$ locate bin/zip
```

`locate` will search its database of pathnames and output any that contain the string