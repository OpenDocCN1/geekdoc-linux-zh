# Working with Directories

![](bbox=[0.137, 0.11, 0.715, 0.358])

Figure 1.7 documents/letters

You can get up to your home directory by using a single `cd` command to go up directories as shown:

```
$ cd ../
$ pwd
/users/steve
$ 
```

Or you can get back to the home directory by a full pathname rather than a relative one:

```
$ cd /users/steve
$ pwd
/users/steve
$ 
```

Finally, there is a third way to get back to the home directory that is also the easiest. Typing the command `cd` without an argument `always` moves you back to your home directory, no matter where you are in the file system:

```
$ cd
$ pwd
/users/steve
$ 
```

# More on the ls Command

When you type the `ls` command, the files in the current working directory are listed. You can also use `ls` to obtain a list of files in other directories by supplying an argument to the command. First's get back to your home directory:

```
$ cd
$ pwd
/users/steve
$ 
```