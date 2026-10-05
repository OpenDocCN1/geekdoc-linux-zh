
/usr/share/doc Documentation ACCESS PERMISSIONS 215

/usr/share/info GNU info system's primary directory

/usr/share/man Online manuals

+   /usr/src Source code Variable data Files with contents that vary as the system runs are kept in subdirectories under /var/. The most common examples are temporary files

## ACCESS PERMISSIONS

Ubuntu Linux supports two methods of controlling who can access a file and how they can access it: traditional Linux access permissions and Access Control Lists (ACLs). This section describes traditional Linux access permissions. See page 221 for a discussion of ACLs, which provide finer-grained control of access permissions than do traditional access permissions.

Three types of users can access a file: the owner of the file (owner), a member of a group that the file is associated with (group; see page 492 for more information on groups), and everyone else (other). A user can attempt to access an ordinary file in three ways: by trying to read from, write to, or execute it.

## ls -l: DISPLAYS PERMISSIONS

When you call ls with the -l option and the name of one or more ordinary files, ls displays a line of information about the file. The following example displays for two files. The file letter.0610 contains the text of a letter, and check_spell contains a shell script, a program written in a high-level shell programming-language:

| Type of file | File access Permissions | ACL | Links | Owner | Group | Size | Date and time of modification | Filename |
|---|---|---|---|---|---|---|---|---|
| -rw-xr-x- | | | 3 | max | pubs | | 2010-08-12 13:15 | memo |

Figure 6-12 The columns displayed by the ls -l command

$ ls -l letter.0610 check_spell
-rw-xr-x- 1 max 852 2010-07-31 13:47 check_spell
-rw-r--r-- 1 max 3355 2010-06-22 12:44 letter.0610

From right to left, the lines that ls -l command contain the following information (refer to Figure 6-12, preceding page):

- The type of file (first character)
- The file access permissions (next nine characters)
- The ACL flag (if the file has an ACL, page 221)
- The number of links to the file (page 226)
- The name of the owner of the file (usually the person who created the file)
- The name of the group the file is associated with
- The size of the file in characters (bytes)
- The date and time the file was created or last modified
- The name of the file

The type of file (first column) for letter.0610 is a hyphen (--) because it is an ordinary file (directory files have a d in this column).

The next three characters specify the access permissions for the owner of the file: r indicates permission, w writes permission, and x execute permission. A – in a column indicates that the owner does not have the permission that could appear in that position.

In a similar manner the next three characters represent permissions for the group, and the final three characters represent permissions for other (everyone else). In the preceding example, the owner of letter.0610 can read and write to the file, whereas the group and others can only read from the file and no one is allowed to execute it. Although execute permission can be allowed for any file, it does not make sense to execute a file that contains a document, such as a letter. The check_spell is an executable shell script, so execute permission is appropriate for it. (The owner, group, and others have permission.)

## chmod: Changes Access Permissions

The Linux file permission scheme lets you give other users access to the files you want to share keep your private files confidential. You can allow others to read and write to a file (handy if you are one of several people working on a joint project). You can allow others only to read from a file (perhaps a project specification you are proposing). Or you can allow others only to write to a file (similar to an inbox or mailbox, where you want to be able to send you mail but do not want them to read your mail). Similarly you can protect directories from being scanned (covered shortly).

## A user with root privileges can access any file on the system

security There is an exception to the access permissions described in this section. Anyone who gains root privileges has full access to all files, regardless of the file's owner or access permissions.

The owner of a file controls which users have permission to access the file and how others can access it. When you own a file, you can use the chmod (change mode) utility to change access permissions for that file. You can specify symbolic (relative) or numeric (absolute) arguments to chmod.

## SYMBOLIC ARGUMENTS TO chmod

The following example, which uses symbolic arguments to chmod, adds (+) read and write permissions (rw) for all (a) users:

```
$ ls -l letter.0610
-rw-rw---- max 3355 2010-06-22 12:44 letter.0610
$ chmod a+rw letter.0610
$ ls -l letter.0610
-rw-rw-r-- 1 max 3355 2010-06-22 12:44 letter.0610
```

Using symbolic arguments, many people remember that UGO stands for user, group, and other. In the following example, chmod removes (-) read and write permissions from all (a) users:

```
$ ls -l letter.0610
-rw-rw---- max 3355 2010-06-22 12:44 letter.0610
$ chmod a-rw letter.0610
$ ls -l letter.0610
-r--r--r-- 1 max 3355 2010-06-22 12:44 letter.0610
```

Another example, chmod adds (+) execute permission to all (a) users:

```
$ ls -l letter.0610
-r--r--r-- 1 max 3355 2010-06-22 12:44 letter.0610
$ chmod a+x letter.0610
$ ls -l letter.0610
-r-xr-xr-x 1 max 3355 2010-06-22 12:44 letter.0610
```

## NUMERIC ARGUMENTS TO chmod

You can also use numeric arguments to specify permissions, instead of letters. The numeric arguments comprise octal digits. The first digit specifies permissions for the owner, the second for group, and the third for other. In the following example, chmod changes only the owner permissions, regardless of how they were previously set:

```
$ ls -l letter.0610
-rw-rw--r-- 1 max 3355 2010-06-22 12:44 letter.0610
$ chmod 600 letter.0610
$ ls -l letter.0610
-rw------- 1 max 3355 2010-06-22 12:44 letter.0610
```

Next, 7 (4 + 2 + 1) gives the owner read, write, and execute permissions. The 5 (4 + 1) gives the group and other users read and execute permissions:

```
$ chmod 755 check_spell
$ ls -l check_spell
-rwxr-xr-x 1 max 852 2010-07-31 13:47 check_spell
```

Refer to Table 6-2 for more examples of numeric permissions.

## Table 6-2 Examples of numeric permissions

| Mode | Meaning |
|---|---|
| 777 | Owner, group, and others can read, write, and execute file |
| 755 | Owner can read, write, and execute file; group and others can read and execute file |
| 711 | Owner can read, write, and execute file; group and others can execute file |
| 644 | Owner can read and write file; group and others can read file |
| 640 | Owner can read and write file, group can read, and cannot access file |

## SETUID AND SETGID PERMISSIONS

When you execute a file that has setuid (user ID) permission, the process executing the file takes on the privileges of the file's owner. For example, if you run a
