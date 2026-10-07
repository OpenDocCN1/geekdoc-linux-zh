As you saw at the outset, **mv** and **cp** are very simple commands. It’s specifying the files that is the complicated part! If things still seem confusing, don’t worry. Even experts sometimes mess up “simple” moves and copies. Follow the examples and try any different ways you can think of. There is a definite logic as to how the files to be moved and copied should be specified. It takes a while to become familiar with this logic, and you will probably have to practice a while before these things become intuitive.

# ## Moving Directories

To move a directory, use the **mv** command. The syntax is **mv** _<directory>_<destination>_. In the following example, let’s move the **newdir** subdirectory found in your current directory to the _/tmp_ directory:

```
```
darkstar:~$ mvdir newdir /tmp
darkstar:~$ cd /tmp
darkstar:/tmp$ ls
/newdir
```
```

The directory **newdir** is now a subdirectory of _/tmp_.

When you move a directory, all its files and subdirectories go with it.

You can use the **mv** command to rename a directory without moving it. For example, if you want to rename the directory **newdir** to **olddir** without copying it, the command

```
```
mv newdir olddir
```
```

does the task. All the files in **newdir** now are under **olddir**.

# ## Removing Files and Directories

Now that you know how to create files and directories, it’s time to learn how to undo your handiwork.

To remove (or delete) a file, use the **rm** command (**rm** is a very terse spelling of _remove_). The syntax is **rm** _<filename>_. For example, the command:

```
```
darkstar:~$ rm dead_duck
```
```

removes the file **dead_duck** from your current directory.

```
```
darkstar:~$ rm /tmp/dead_duck
```
```

removes the file **dead_duck** from the _/tmp_ directory.

You can use wildcards with the **rm** command, just as with all other Linux commands. This can cause you a lot of problems if you type the command at the wrong location.