
the preceding criteria are met. If no action criteria appear in the *expression*, -print is assumed by default. Refer to the following “Discussion” and “Notes” sections.

-exec command\; The file evaluated meets this criterion if the command returns a zero (*true*) value as an exit status. You must terminate the command with a semicolon. a pair of braces {} within the command represents the name of the file being evaluated. You can use the -exec action criterion at the end of a group of other criteria to execute the command if the preceding criteria are met. Refer to “Discussion.” See xargs on page 1377 for a more efficient way of doing what this option does.

-ok command\; This action is the same as -exec but displays each command to be executed enclosed in angle brackets and executes the command only if it receives a y or Y from standard input.

-depth The file evaluated meets this criterion. It causes find to act on entries in a directory before it acts on the directory itself. When you use find to send files to cpio utility, the -depth criterion enables cpio to preserve modification times of directories (assuming you use the --preserve-modification-time option to cpio). See “Discussion” and “Examples” on pages 1126 and 1127.

-xdev The file evaluated meets this criterion. It causes find not to search directories in filesystems other than the one in which the working directory (from the directory-list argument) resides. Also -mount.

-nouser The file evaluated meets this criterion if it does not belong to a user who is in the /etc/passwd file (that is, the user ID associated with the file does not correspond to a known user of the system).

-nogroup The file evaluated meets this criterion if it does not belong to a group that is listed in the /etc/group file.

-follow When this criterion is specified and find encounters a symbolic link pointing to a directory file, find follows the link.

# Discussion

Assume that x and y are criteria. The following command line never tests criterion y if it does not meet criterion x. Because the criteria are separated by a SPACE (the Boolean AND operator), one finds that criterion x is not met, the file cannot meet the criteria, so find does not continue testing. You can read the expression as “(test to see) whether the file meets criterion x and (SPACE means and) criterion y”:

```
$ find dir x y
```

The next command line tests the file against criterion y if criterion x is not met. The file can still meet the criteria, so find continues the evaluation. It is read as “(test to see) whether criterion x or criterion y is met.” If the file meets criterion x, it does not evaluate criterion y, as there is no need:

```
$ find dir x -or y
```

Certain "criteria" do not select files but cause find to take action. The action is triggered when find evaluates one of these action criteria. Therefore, the position of an action on the command line, not result of its evaluation, determines whether find takes the action.

The -print action criteria causes find to display the pathname of the file it is testing. The following command line displays the names of all the files in the directory (and all its subdirectories), where they meet the criterion x:

```
$ find dir -print x
```

The following command line displays only the names of the files in the directory meets criterion x:

```
$ find dir x -print
```

This common use of -print after the testing criteria is the default action criterion. The following command line does the same thing as the previous one:

```
$ find dir x
```

# Note

You can use the -a operator between criteria for clarity. This operator is a Boolean AND operator, just as the SPACE is.

# Examples

The following command line finds the files in the working directory and subdirectories that have filenames that begin with a. The command uses a period to designate the working directory. To prevent the shell from interpreting the ambiguous file reference, it is enclosed within quotation marks:

```
$ find . -name 'a*'
```

If you omit the directory-list argument, find searches the working directory. The following command line performs the same function as the preceding one without specifying the working directory:

```
$ find -name 'a*'
```

The following command line sends a list of selected filenames to the cpio utility, which writes them to tape. The first part of the command line ends with a pipe symbol, so the shell expects another command to follow and displays a secondary prompt (>) before accepting the rest of the command line. You can read command as "find, in the root directory and all subdirectories (/), ordinary files (-type f) that have been modified within the past day (-mtime -1), with the exception of files whose names are suffixed with .o (-name '*.o')." (An object file .o suffix and usually does not need to be preserved as it can be recreated by the corresponding program source file.

```
$ find -type f -mtime -1 -name '*.o' -print |
 cpio -oB /dev/cpio
```

The following command find lines, displays the filenames of, and deletes the files in the working directory and subdirectories named core or junk:

```
$ find . \( -name core -o -name junk \) -print -exec rm {} \;
```

The parentheses and the semicolon following -exec are quoted so that the shell does not treat them as special characters. SPACES separate the quoted parentheses from other elements on the command line. Read this command as "find, in the working directory and subdirectories (,), files named core (-name core) or (-o) junk (-name junk) [if a file meets these criteria, continue with] and (SPACE) print the name of the file (-print) and delete the file (-exec rm {})."

The next script uses find with grep to identify files that contain a particular string. This script enables you to look for a file when you remember its content but cannot remember its filename. The finder script locates files in the working directory and subdirectories that contain the string specified on the command line. -type f criterion is necessary so that find passes grep only the names of ordinary files, not directories:

```
$ cat finder
find -type f -exec grep -l "$1" {} \;
$ finder "Executive Meeting"
./january/memo.0102
./april/memo.0415
```

When called with the string Executive Meeting, finder locates two files containing string: ./january/memo.0102 and ./april/memo.0415. The period (.) in the pathnames represents the working directory; that is, january and april are subdirectories of the working directory.

The next command in user directories finds the files that are larger than 100 and have been accessed more than five days (-atime +5). -ok asks whether you want to delete. You must respond to each of these with y (for yes) or n (for no). In the next example, /home/alex/memos is a symbolic link to Jenny's directory. When you use the -follow option, the symbolic link is followed and the contents of that directory are searched:

```
$ ls -l /home/alex
1rwxrwx 1 alex pubs 19 17:07 memos -> /home/jenny/memos
-rw-r-- 1 alex pubs 19 17:08 report
```

```
$ find /home/alex -print
/home/alex
/home/alex/memos
/home/alex/report
/home/alex/.profile
```

```
$ find /home/alex -follow -print
/home/alex
/home/alex/memos
/home/alex/memos.817
/home/alex/memos.710
/home/alex/report
/home/alex/.profile
```

# finger

Displays information about users

The finger utility displays the login names of users, together with their full names, terminal device numbers, the times they logged in, and other information. The options control how much information finger displays, and the user-list specifies which users finger displays about.

# Arguments

Without any arguments, finger provides a short (-s) report on users who are logged in on the local system. When you specify a user-list, finger provides a long (-l) report on each of the users in the user-list.

If the name includes an at sign (@), the finger utility interprets the name following the @ as the name of a remote host to contact over the network. If there is also a name in front of the @ sign, finger provides information on that particular user on the remote system.

# Options

+   -l long Displays detailed information (the default display when user-list is present).
-m match If a user-list is specified, displays entries only for those users whose login names match the names given in user-list. Without the user-list names match login and full names.
-p plan and project Does not the contents of .plan and .project files for users. Because these files may escape sequences that can change the behavior of your display, you may not wish to view them. Normally the long listing of finger shows you the contents of these files if they exist in the user's home directory.
-s short Provides a short report for each user. Same as no options and no user-list.

# Discussion

The long report provided by the finger utility includes the user's login name, fullname, home directory location, and login shell, followed by information about when the user last logged in on the system and how long it has been since the user
