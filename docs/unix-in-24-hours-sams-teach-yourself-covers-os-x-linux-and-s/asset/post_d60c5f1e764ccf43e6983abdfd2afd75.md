
```
% ls -l bin/my.new.cmd
-rwxr-x-- 1 taylor      0 Oct 11 15:07 bin/my.new.cmd
% my.new.cmd
%
```

Voilà! You’ve created your first Unix command, which is an achievement even though it doesn’t do much. You can now see how the search path and the Unix philosophy of having applications be identical to regular files, except for the permission can be invaluable as you learn how to customize your environment.

Execute permission enables the user to run a file as if it were a program. Execute permission is independent of other permissions granted—or denied—so it’s perfectly feasible to have a program with read and execute permission but no write permission. (After all, you wouldn’t want others altering the program itself.) You also can have programs with execute permission only. This means that users can run the application, but they can’t examine it to see how it works or copy it. (Copying requires the ability to read the file contents, of course.)

## Note

Though actual programs with execute-only permission work fine, a special class of programs called shell scripts fail. Shell scripts act like a Unix command-line macro facility, which enables you to easily save a series of commands in a file and then run them as a single program. To work, however, the shell must be able to read the file and execute it, too, so shell scripts always require both read and execute permission.

There are clearly quite a few permutations on the three different permissions: read, write, and execute. In practice, a few occur most commonly, as listed in Table 5.2.

| Permission | Meaning |
|---|---|
| --- | No access is allowed |
| r-- | Read-only access |
| r-x | Read and execute access, for programs and shell scripts |
| rw- | Read and write access, for files |
| rwx | All access allowed, for programs |

## TABLE 5.2 The Most Common File Permissions

These permissions have different meanings when applied to directories, but --- always indicates that no one can access the file in question.

Interpretation of the following few examples should help:

Click here to view code image

```
-rw--- 1 taylor    3843 Oct 10 16:22 iecc.list
-rw-rw-r 1 taylor  280232 Oct 10 16:22 mailing.lists
-rw-rw- 1 taylor   1031 Oct  7 15:44 newlists
-rwxr-x- 1 taylor    64 Oct  9 09:31 the.script
```

The first file, iecc.list, has read and write permission for the owner (taylor) and is off-limits to all other users. The file mailing.lists offers similar access to the file owner (taylor) and to the group, but it offers read-only access to everyone else on the system. The third file, newlists, provides read and write access to both the file owner and group but no access to anyone not in the group.

The fourth file on the list, the.script, is a program that can be run by both the owner and group members, read (or copied) by both the owner and the group, and written (altered) by the owner. In practice, this probably would be a shell script, as described earlier, and these permissions would enable the owner (taylor) to use an editor to modify the commands therein. Other members of the group could read and use the shell script but would be denied access to change it.

## Task 5.2: Directory Permissions Settings

Directories are similar to files in how you interpret the permissions strings. The differences occur because of the unique purpose of directories—namely, to store other files or directories. I always think of directories as bins or boxes. You can examine the box itself, or you can look at what’s inside.

In many ways, Unix treats directories simply as files in the file system, where the content of the file is a list of the files and directories stored within rather than a letter, program, or shopping list.

The difference, of course, is that when you operate with directories, you’re operating both with the directory itself and, implicitly, with its contents. By analogy, when you fiddle with a box full of toys, you’re not altering just the state of the box itself but also potentially the toys within.

Three permissions are possible for a directory, just as for a file: read, write, and execute. The easiest is write permission. If a directory has write permission enabled, you can add new items to and remove items from the directory. It’s like owning the box; you can do what you like with the toys inside.

The interaction between read and execute permission with a directory is confusing. There are two types of operations you perform on a directory: listing the contents of the directory (usually with ls) and examining specific known files within the directory.

- 1. Start by listing a directory, using the -d flag:

Click here to view code image

```
$ ls -ld testme
dr-x--- 2 taylor 512 Oct 11 17:03 testme/
$ ls -l testme
total 0
-rw-rw-- 1 taylor 0 Oct 11 17:03 file
$ ls -l testme/file
-rw-rw-- 1 taylor 0 Oct 11 17:03 testme/file
```

For a directory with both read and execute permission, you can see that it’s easy to list the directory, find out the files therein, and list specific files within the directory.

- 2. Read permission on a directory enables you to read the “table of contents” of the directory but, by itself, does not allow you to examine any of the files therein. By
