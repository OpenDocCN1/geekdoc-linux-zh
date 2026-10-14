
## 6.1.3 Listing the Members of a Group

There are two methods for listing the members of a particular group.

### METHOD #1

Members
DEB: members

Use the members tool to list the members of a particular group. Give the name of the particular group as an argument.

⇒ To output a list of the members of the galley group, type:

```
$ members galley [RET]
captain steward pete
$
```

In this example, three usernames are output, indicating that these three users are the members of the galley group.

NOTES: The members tool is not yet widely available outside of the Debian distribution; if you can't locate a copy, you can always install the sources from the Debian package (see Recipe 1.1.2 [Preparation of Recipes], page 3).

### METHOD #2

On systems without members conveniently installed, the members of a particular group may be listed by using grep in conjunction with cut. First, use grep to output the line in /etc/group whose first field matches the particular group name, and pipe the output to cut to output only the last field, containing the list of users who belong to that group.

⇒ To list all members of the crew group, type:

```
$ grep ^crew: /etc/group | cut -d : -f 4 [RET]
```

NOTES: For more information on grep and cut, see Recipe 14.1 [Searching Text for a Word], page 333 and Recipe 13.7.4 [Removing Columns from Text], page 324, respectively.

⇒ To give group ownership of the maps directory and all the files it contains to the bridge group, type:

```
$ chgrp -R bridge maps [RET]
```

## 6.3 Controlling Access to Files

Each file has a set of permissions that specify what type of access that different users have to the file. There are three kinds of permissions: read, write, and execute. You need read permission for a file to read its contents, write permission to write changes to or remove the file, and execute permission to run the file as a program.

Normally, users have write permission only for files in their own home directories. Only the superuser has write permission for the files in important directories, such as /bin and /etc—so as a regular user, you never have to worry about accidentally writing to or removing an important system file.

Permissions work differently for directories than for other kinds of files. Read permission for a directory means that you can see the files in the directory; write permission lets you create, move, or remove files in the directory; and execute permission lets you use the directory name in a path (see Chapter 5 [Files and Directories], page 125).

If you have read permission but not execute permission for a directory, you can only read the names of files in that directory—you can't read their other attributes, examine their contents, write to them, or execute them. With execute but not read permission for a directory, you can read, write to, or execute any file in the directory, provided that you know its name and that you have the appropriate permissions for that file.

Each file has separate permissions for three categories of users: the user who owns the file, all other members of the group that owns the file, and all other users on the system. If you are a member of the group that owns a file, the file's group permissions apply to you (unless you are the owner of the file, in which case the user permissions apply to you).

When you create a new file, it has a default set of permissions—usually read and write for the user, and read for the group and all other users. (On some systems, the default permissions are read and write for both the user and group, and read for all other users.)

The file access permissions for a file are collectively called its access mode. The following sections describe how to list and change file access modes, including how to set the most commonly used access modes.

**NOTES:** The superuser, `root`, can always access any file on the system, regardless of its access permissions.

For more information on file permissions and access modes, see the `fileutils` Info documentation (see Recipe 2.8.5 [Reading an Info Manual], page 48).

### 6.3.1 Listing the Permissions of a File

To list a file's access permissions, use `ls` with the `-l` option (see Recipe 5.3.3 [Listing File Attributes], page 136). File access permissions appear in the first column of the output, after the character for file type.

For example, consider the verbose listing of the file `cruise`:

```
-rwxrwxr--  1 captain  crew  8,420 Jan 12 21:42 cruise
```

The first character (`-`) is the file type; the next three characters (`rwx`) specify permissions for the user who owns the file; and the next three (`rw-`) specify permissions for all members of the group that owns the file except for the user who owns it. The last three characters in the column (`r--`) specify permissions for all other users on the system.

All three permissions sections have the same format, indicating, from left to right, read, write, and execute permission with "r", "w", and "x" characters. A hyphen (-) in place of one of these letters indicates that permission is not given.

In this example, the listing indicates that the user who owns the file, `captain`, has read, write, and execute permission, and the group that owns the file, `crew`, has read and write permission. All other users on the system have only read permission.

### 6.3.2 Changing the Permissions of a File

To change the access mode of any file you own, use the `chmod` ("change mode") tool. It takes two arguments: an operation, which specifies the permissions to grant or revoke for certain users, and the names of the files to work on.

To build an operation, first specify the category or categories of users as a combination of the following characters:

- u The user who owns the file.
- g All other members of the file's group.
- o All other users on the system.
