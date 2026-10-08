
# Table 5.1. The ls file type indicators.

| Letter | Indicated File Type |
|---|---|
| d | Directory |
| b | Block-type special file |
| c | Character-type special file |
| l | Symbolic link |
| p | Pipe |
| s | Regular file |

The next nine letters in the permissions string are broken into three groups of each—representing the owner, group, and everyone—is just like everything else—as shown in Figure 5.1.

# Figure 5.1. Interpreting file permissions.

![](img/f32f6f53c129de2ebafcd2b4ff01b1c9_100_0.png)

To understand what the permissions mean to the computer system, remember that UNIX treats everything as a file. If you install an application, it's just like everything else, with one exception: the system knows that an application is executable. A letter to your Mum is a regular file, but if you were to tell UNIX that it was executable, the system would merely try to run it as a program (and fail).

There are three primary types of permission for files: read, write, and execute. Read permission enables you to examine the contents of the file with a variety of different programs, but they cannot alter, modify, or delete anything. They can copy the file and edit it the new version, however.

Write permission is the next step. Users with access to a file can add information to the file. If you have write and read permission for a file, you can edit it—the read permission enables you to view the contents, and the write permission lets you alter them. With write permission only, you'd be able to add information to the file, but you wouldn't be able to view the contents of the file at any time. Admittedly, write-only permission is unusual in UNIX, but you might see it for log files, which are files that track activity on the system. If each time you logged into your UNIX system the computer recorded the fact, noting who logged in, where they logged in from, and the current time and date. Armed with that information, you could ascertain who last logged in, who uses dial-up phone lines, and who uses the computer most. (In fact, there's a UNIX command that just does that. It's called last.)

So far you've learned that you can have files with read-only permission, read-write permission, and write-only permission. The third type of access permission is execute, noted by ls -l with an x in the third slot of the permissions string.

```
% ls -l bin
total 57
-rw-r---- 1 taylor 1507 Aug 17 13:27 bounce.msg
-rw-r---- 1 taylor 32916 Oct 10 19:09 calc
-rw-r---- 1 taylor 18567 Sep 14 22:14 fixit
-rw-r---- 1 taylor 334 Oct 01 09:53 punt
-rw-r---- 1 taylor 3424 Sep 10 22:27 rumor.mill.sh
```

![](img/f32f6f53c129de2ebafcd2b4ff01b1c9_101_0.png)

- 1. Try listing the files in the directory /etc on your system, and if you can identify which executable files or programs, which are directories, are symbolic links (denoted with an i as the first character of the permissions string; they're files that point to other files or directories that point to other directories), and which are regular files.
- 2. Execute permission is slightly different from either read or write permission. If the directory containing the file is in your search path (the value of environment variable PATH), any file that has execute permission is automatically started each time filename is entered, regardless of where you are in the file system.

```
% pwd
%users/taylor
% env PATH
%users/taylor/bin:/bin:/usr/ucb:/usr:/usr/local/bin:
% ls -l bin/say.hi
-rw-r---- 1 taylor 9 Oct 11 13:32 say.hi
% hi
```

You can now see the importance of your search PATH. Without a search PATH, the system wouldn't be able to find any commands, and would be left with a functional system. You can also see the purpose of checking the execute permission status. I'm going to jump ahead a bit to show you use of chmod so you can see what happens if I remove the execute permission from the say.hi program:

```
% chmod -x bin/say.hi
% ls -l bin/say.hi
-rw------- 1 taylor 9 Oct 11 13:32 say.hi
% say.hi
/users/taylor/bin/say.hi: Permission denied.
```

This time UNIX searched through my path, found a file that matched the name of the program I requested, and then ascertained that it wasn't executable.

- 3. Now try entering say.hi on your computer system. You'll get a different error message: Command not found, which tells you that UNIX searched all the directories in your path but couldn't find a match.
- 4. Check your PATH and find a directory that you can add files in. You'll probably have a bin directory in your home directory. That's a good place to add a file using the touch command:

```
% env PATH
/users/tail/bin:/bin:/usr/ucb:/usr:/usr/local/bin:
% touch my.new.cmd
% ls -l bin
-rw-r---- 1 taylor 0 Oct 11 15:07 my.new.cmd
```

- 5. Now try to execute the command by entering its name directly:

```
% my.new.cmd
/users/tail/bin/my.new.cmd: Permission denied.
```

![](img/f32f6f53c129de2ebafcd2b4ff01b1c9_102_0.png)

If you're using the C Shell as your interpreter, it probably won't find the command you created. This is because, to speed things up, it keeps an internal table of commands. You need to force the program to rebuild its table, and when you enter the filename, don't get permission denied but instead see Command not found, try again.

- 6. Finally, use chmod to add permission to the file, and try it one more time.

```
% chmod +x bin/my.new.cmd
% ls -l bin/my.new.cmd
-rw-r-x 1 taylor 0 Oct 11 15:07 my.new.cmd
% my.new.cmd
```

Voila! You've created your first command, even though it doesn't do much. You can now see the search path and the UNIX philosophy of having applications identical to regular files, except for the permission, can be invaluable as you learn to customize your environment.

![](img/f32f6f53c129de2ebafcd2b4ff01b1c9_102_1.png)

# SUMMARY
Execute permission enables the user to run the file as if it were a program. Execute permission is independent of other permissions granted—or denied—so it's perfectly feasible to have a program with read and execute permission, but no write permission (After all, you wouldn't want others altering the program itself.). You also can have programs with execute permission only. This means that users can run the application, but they can't examine it to see how it works or copy it. (Copying requires the ability to read the file.)

![](img/f32f6f53c129de2ebafcd2b4ff01b1c9_103_0.png)

# JUST A Minute
Though actual programs with execute-only permission work fine, a special class of programs called shell scripts fail. Shell scripts act like a UNIX command-line macro facility, which enables you to save easily a series of commands in a file and then run them as a single program. To work, however, the shell must be able to read the file and execute it, too, so shell scripts always require both read and execute permissions.

There are clearly a few permutations on the different permissions: read, write and execute. In practice, a few occur most commonly, as listed in Table 5.2.

# Table 5.2. The most common file permissions.

| Permission | Meaning |
|---|---|
| --- | No access is allowed |
| r-- | Read-only access |
| r-x | Read and execute access, for programs and shell scripts |
| rw- | Read and write access, for files |
| rwx | All access allowed, for programs |

These permissions have different meanings when applied to directories, but --- always indicates that no one can access the file in question.

Interpretation of the following examples should help:

```
---r-- 1 taylor 3843 Oct 10 16:22 iecc.list
---rw-- 1 taylor 280233 Oct 10 16:22 mailing.lists
---rw-- 1 taylor 1031 Oct 7 15:44 newlists
---rwx-x-- 1 taylor 64 Oct 9 09:31 the.script
```

The first file, iecc.list, has read and write permission for the file owner (taylor) and is off-limits to all other users. The file mailing.lists offers similar access to the file owner (taylor) and the group but offers read-only access to everyone else on the system. The third file, newlists, provides read and write access to both the file owner and group, but no access to anyone not in the group.
