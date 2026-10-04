point for any files it accesses with a relative pathname. Unless a process makes specific arrangements to set up a particular current working directory for itself (and most don’t) the default will be the directory that the user was in when the program was started.

What about trying to specify the relative pathname to the file a from the directory /home/mike? The problem here is that /home/mike and a are in different branches of the directory tree. In order to solve this problem you need to know about two extra names that are automatically included in every Linux directory. They are called . (pronounced dot) and .. (pronounced dot-dot). The name dot is an alias for the current directory and dot-dot is an alias for the parent of the current directory, allowing you to go back up the tree when specifying relative path names. Given the dot-dot notation, the answer to the previous question involves going back up the tree from /home/mike to /home and then back down the right branch to the file a. This would give the relative pathname as:

```
../lynne/proj1/a
```

Incidentally, even though the root directory does not have a parent directory, it still contains the name dot-dot, which is made to point back to the root directory itself. So, in effect, the root directory is treated specially in that it is its own parent. This also means that it is not an error to specify a relative pathname with too many dot-dots in it.

# 1.3 Exploring the File Hierarchy

When you login, there is a special directory associated with your login name called your home directory. Your home directory is actually your initial current working directory. It is the directory that acts as the starting point (the root if you like) for the part of the overall directory tree that belongs to you. All the files and directories that you create as a part of any work you do on the system will generally be located under your home directory.

The simplest way to find out where in the directory hierarchy your home directory is located is just to use the command pwd straight after you login. The pwd command tells you your present working directory. This is the directory you are currently ‘in’, which will be your home directory when you first login. Using the pwd command from your home directory will give output like this:

```
$ pwd
/home/you
```

where /home/you will be replaced by the absolute pathname to your home directory. In order to move your present working directory away from your home directory to somewhere else in the directory hierarchy, you use the cd (change directory) command. So, to change directory to the directory hierarchy's root directory you would use the command: