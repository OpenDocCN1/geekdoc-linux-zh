
umask This predetermined default file and directory permission set is used as a reference when new files or directories are created in the file system.

### Exercises

1. In what situations might the following file permissions be useful?

Click here to view code image

```
r--r--r--
-rw--w--w-
rwxr-xr-x

r--r--rw-
--w--w--
r--x--x--x
```

2. Translate the six file permissions strings in question 1 into their binary and numeric equivalents.

3. Explain what the following umask values would make the default permissions for newly created files:

```
007   077   777
111   222   733
272   544   754
```

4. Count the number of groups that are represented by group membership of files in the tmp directory on your system. Use id to see whether you’re a member of any of them.

5. Which of the following directories could you modify if the id command listed the following information? Which could you view using the ls command?

Click here to view code image

```
% id
uid=19(smith) gid=50(users) groups=50(users)
% ls -lGF
 drw-r--r-- 2 root users 512 Oct 12 14:52 sh/
drwxr-xr-x 2 shakes root 512 Oct 12 07:23 shakes/
drw--- 2 meademd com435 1024 Oct 12 14:46 tmp/
drwxr-x- 3 smith users 512 Oct 12 12:37 viewer/
drwx-- 3 jin users 512 Oct 12 12:37 Zot!/
```

### Preview of the Next Hour

In the next hour, you’ll learn the various Unix file-manipulation commands, including how to copy files, how to move them to new directories, and how to create new directories. You’ll also learn how to remove files and directories as well as about the dangers of file removal on Unix.

## Hour 6. Creating, Moving, Renaming, and Deleting Files and Directories

### Goals for This Hour

In this hour, you will learn

- How to create new directories using `mkdir`
- How to copy files to new locations using `cp`
- How to move files to new locations using `mv`
- About renaming files using `mv`
- How to remove directories using `rmdir`
- How to remove files using `rm`
- About minimizing the danger of using the `rm` command

In this hour, you’ll learn the basic Unix file-manipulation commands. You’ll learn how to create directories with `mkdir`, remove directories with `rmdir`, use `cp` and `mv` to move files about in the file system, and use `rm` to remove files. The `rm` command can be dangerous; this hour you’ll learn that there isn’t an “unremove” command in Unix, and you’ll also learn how to circumvent the possible dangers that lurk in the program.

This hour introduces several tremendously powerful commands that enable you to create a custom file-system hierarchy (or wreak unintentional havoc on your files). As you learn these commands, you’ll also read hints and ideas on how best to use the Unix file system to keep your files neat and organized.

### Manipulating the Unix File System

You know how to find out what files are where in the file system, using `ls`, but there are also some incredibly useful commands that let you manipulate and modify files, directories, and the file system itself. That’s what we’ll focus on here.

### Task 6.1: Creating New Directories Using mkdir

One important aspect of Unix that has been emphasized continually in this book is that, as in all other modern operating systems, in Unix the file system is hierarchical. The Unix file system includes directories containing files and directories, and each of those directories can contain yet more files and directories. Your own home directory, however, probably doesn’t yet contain any directories (except . and .. of course, because they’re built-in shortcuts to the current and parent directory, respectively), which prevents you from exploiting what I call the virtual file cabinet of the file system.

Working with cloud storage? Me too. Turns out, though, that what you have stored in the cloud shows up on a Unix system as just more files and directories, with more files and directories within those. This is true with Dropbox, OneDrive, iCloud, and any other Unix-compatible cloud storage system you might have configured, even those internal to your corporation. I'll show you what I mean later in the lesson!

The command for creating directories is actually one of the least complex and most mnemonic (for Unix, anyway) in this book: mkdir, for “make directory.”

Note

Pronounce the mkdir command as “make-drrr.”

1. Move to your home directory and examine the files and directories there. Here’s an example:

Click here to view code image

```
% cd
% ls -F
Archives/          OWL/               rumors.26Oct.Z
InfoWorld/         PubAccessLists.Z   rumors.5Nov.Z
LISTS              bin/               src/
Mail/              educ
News/              mailing.lists.bitnet.Z
```

2. To create a directory, specify what you’d like to name the directory and where you’d like to locate it in the file system (the default location is your current working directory):

Click here to view code image

```
% mkdir NEWDIR
% ls -F
Archives/          News/              mailing.lists.bitnet.Z
InfoWorld/         OWL/               rumors.26Oct.Z
LISTS              PubAccessLists.Z   rumors.5Nov.Z
Mail/              bin/               src/
NEWDIR/            educ
```

Note

Although Unix is very flexible about file and directory names, as a general rule, you’ll want to avoid spaces, tabs, control characters, and the / character because they’ll make things more difficult later on.

3. That’s all there is to it. You’ve created your first Unix directory, and you can now list it with ls to see what it looks like:

Click here to view code image

```
% ls -ld NEWDIR
drwxrwx- 2 taylor     24 Nov  5 10:48 NEWDIR
% ls -la NEWDIR
total 2
drwxrwx- 2 taylor     24 Nov  5 10:48 .
drwx-- 11 taylor    1024 Nov  5 10:48 ..
```

Remember that the -d flag to ls specifies that it should show the directory itself, not the contents of the directory. Try it both ways, and you’ll immediately see the
