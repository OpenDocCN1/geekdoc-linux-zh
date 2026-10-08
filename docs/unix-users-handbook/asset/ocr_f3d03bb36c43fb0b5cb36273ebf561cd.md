![](bbox=[0.05, 0.09, 0.13, 0.17])

# ## rmdir - Remove directories.

Options

+   -   -i
    Interactive remove whereby you are prompted to confirm that you wish to remove a directory
-   -f
    Force directories to be removed.
-   -p
    If, after removing a directory, the parent directory is empty, then remove it also. This goes on until a parent directory is encountered that is not empty.

# # Using Commands

# ## Using the cd, pwd, ls, mkdir, and cp Commands

Now that we have covered some of these commands in an "isolated" fashion, let’s put some of the commands together.

![](bbox=[0.05, 0.58, 0.13, 0.66])

Let’s start by viewing the hierarchy of a directory under *denise*’s home directory called **krsort.dir.old**, as shown in Figure 3-7:

![](bbox=[0.05, 0.68, 0.13, 0.76])

```
```text
$ cd /home/denise/krsort.dir.old
$ pwd
/home/denise/krsort.dir.old
$ ls -1
total 168
-rw-r--x     1 denise     users        34592 Oct 27 18:20 krsort
-rwxr-xr-x     1 denise     users         3234 Oct 27 17:30 krsort.c
-rwxr-xr-x     1 denise     users        32756 Oct 27 17:30 krsort.dos
-rw-r--     1 denise     users         9922 Oct 27 17:30 krsort.q
-rwxr-xr-x     1 denise     users         3085 Oct 27 17:30 krsortorig.c
```
```

![](bbox=[0.05, 0.78, 0.13, 0.86])