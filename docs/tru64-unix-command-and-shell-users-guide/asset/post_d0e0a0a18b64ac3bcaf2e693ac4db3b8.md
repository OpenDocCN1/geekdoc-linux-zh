
### 5.4.1.2 Changing Directory Permissions

The procedure for changing directory permissions is the same as that for changing file permissions. However, to list the information about a directory, you use the `ls -ld` command:

```text
$ ls -ld project
drwxr-xr-x  2 larry  system  32 Jun 5 10:07 project
$
```

Now change the permissions with the `chmod g+w` command so that the group (g) has write permission (+w) for the directory project:

```text
$ chmod g+w project
$ ls -ld project
drwxrwxr-x  2 larry  system  32 Jun 5 10:07 project
$
```

### 5.4.1.3 Using Pattern-Matching Characters

If you want to make the same change to the permissions of all entries in a directory, you can use the pattern-matching character (`*`) with the chmod command. For information on pattern-matching characters, see Chapter 2.

In the following example, the command `chmod g+x *` gives execute (x) permission to the group (g) for all files (*) in the current directory:

```text
$ chmod g+x *
$
```

Now enter the `ls -l` command to show that the group now has execute (x) permission for all files in the current directory:

```text
$ ls -l
total 7
-rw-rwxrw-  1 larry  system  101 Jun 5 10:03 file1
-rw-r-xr--  1 larry  system  171 Jun 5 10:03 file2
-rw-r-xr--  1 larry  system  130 Jun 5 10:06 file3
drwxrwxr-x  2 larry  system   32 Jun 5 10:07 project
-rw-r-xr--  1 larry  system    0 Jun 5 11:03 record1
-rw-r-xr--  1 larry  system    0 Jun 5 11:03 record6
drwxr-xr-x  2 larry  system   32 Jun 5 10:31 reports
$
```

### 5.4.1.4 Setting Absolute Permissions

An absolute permission assignment (=) resets all permissions for a file or files, regardless of how the permissions were set previously.

In Example 5-1, the `ls -l` command lists the permissions for the file3 file. Then the `chmod a=rwx` command gives all three permissions (rwx) to all users (a).

**Example 5-1: Setting Absolute Permissions**

```text
$ ls -l file3
-rw-r-xr--  1 larry  system  130 Jun 5 10:06 file3
$ chmod a=rwx file3
$ ls -l file3
-rwxrwxrwx  1 larry  system  130 Jun 5 10:06 file3
$
```

You can also use an absolute assignment to remove permissions. In Example 5-2, the `chmod a=rw file3` command removes the execute permission (x) for all users (a) from the file3 file:

**Example 5-2: Removing Absolute Permissions**

```text
$ chmod a=rw file3
$ ls -l file3
-rw-rw-rw-  1 larry  system  130 Jun 5 10:06 file3
$
```

### 5.4.2 Specifying Permissions with Octal Numbers

You can also use octal numbers to change file and directory permissions.

To use octal number permission codes with the chmod command, enter the command in the following form:

```text
chmod octalnumber filename
```

The octal number entry is a 3-digit octal number that specifies the permissions for owner, group, and others. The filename entry is the name of the file whose permissions you want to change. It can be the name of the file or a list of file names separated by spaces. You may also use pattern-matching characters to specify files. See Section 5.4.1.3 for more information.

An octal number corresponds to each type of permission:

- 4 = read
- 2 = write
- 1 = execute

To specify a group of permissions (a permission field), add together the appropriate octal numbers (r, w, and x denote read, write, and execute respectively):

```text
3 = -wx (2 + 1)
6 = rw- (4 + 2)
7 = rwx (4 + 2 + 1)
0 = --- (no permissions)
```

Table 5–2 lists the eight possible permission combinations.

**Table 5–2: Permission Combinations**

| Octal Number | Binary Number | Permissions | Description |
|---|---|---|---|
| 0 | 000 | None | No permissions granted |
| 1 | 001 | --x | Execute |
| 2 | 010 | -w- | Write |
| 3 | 011 | -wx | Write/execute |
| 4 | 100 | r-- | Read |
| 5 | 101 | r-x | Read/execute |
| 6 | 110 | rw- | Read/write |
| 7 | 111 | rwx | Read/write/execute |

The entire permission code for a file or directory is specified with a 3-digit octal number, one digit each for owner, group, and others. Table 5–3 shows some typical permission codes and how they relate to the permission fields.

**Table 5–3: How Octal Numbers Relate to Permission Fields**

| Octal Number | Owner Field | Group Field | Others Field | Complete Code |
|---|---|---|---|---|
| 777 | rwx | rwx | rwx | rwxrwxrwx |
| 755 | rwx | r-x | r-x | rwxr-xr-x |
| 700 | rwx | --- | --- | rwx------ |
| 666 | rw- | rw- | rw- | rw-rw-rw- |

For example, you could use the following commands to change the permission of file3 using octal numbers:

```text
$ ls -l file3
-rw-rw-rw-  1 larry  system  130 Jun 5 10:06 file3
$ chmod 754 file3
$ ls -l file3
```
