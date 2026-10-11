Finally, to remove a directory, with the special `rmdir` command, first you have to delete all the files inside it, and then you can delete it. To remove all the files in the directory `/home/rich/notes` and delete it at the same time (make sure you really want to do this!), you can type either

```
rm -rf /home/rich/notes
```

or you can type the following series of commands:

```
cd /home/rich/notes
rm *
cd ..
rmdir notes
```

This should be enough to get you started. Happy exploring!

# # A Permissions Primer

If you find yourself scratching your head when looking at parts of that long format file listing in Figure 7-3, don’t worry. It’s just code that describes the permissions assigned to the file. Linux was created as a multi-user operating system – meaning that it assumes more than one person is using the system, and it also assumes you’ll want some type of security on who can (or can’t) mess with your files.

The “Comprehending file types” section earlier gave you a feeling for the first letter on each line, but nine more characters are attached to that item before you get to the next column. This group of nine is the set of *permissions* (also called a *permission set*) for the file or directory. Linux uses these permissions as a way of providing file and directory security by giving you the means to specify exactly who can look at your files, who can change them, and even who can run your pro-grams. You need this capability when you have a bunch of different users on the same machine, networked to the world.

# ## Checking out the triplets

Each permission set consists of three triplets. Each of the triplets has the same basic structure but controls a different aspect of who can use what. Consider the long format listing for `/home/rich` in the following code:

```
total 464
drwx------ 23 rich rich 4096 Dec 15 05:01 .
```