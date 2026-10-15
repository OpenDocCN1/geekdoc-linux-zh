# 5.5.3 Access Privileges for Directories

As previously stated, the read permission on a directory allows you to read the contents of the directory (recall that the contents of a directory are the names of files and directories in it), the write permission allows you to create a file in the directory or remove an existing file or directory from it, and the execute permission for a directory is permission for searching the directory. It is important to note that read and write permissions on directories are not meaningful without the search permission. So, you must have both read and execute permissions on a directory to be able to list its contents. Similarly, you must have both write and execute permissions on a directory to be able to create a file in it.

In the following session, the write permission for the directory courses has been turned off. Thus, you cannot create a subdirectory ee345 in this directory by using the mkdir command or copy a file foo into it. Similarly, as you do not have search permission for the directory personal, you cannot use the cd command to enter (change directory to) this directory. If the directory sample had a subdirectory, say foobar, for which the execute permission was turned on, you still could not change directory to foobar, because search permission for sample is turned off. Finally, as read permission for the directory personal is turned off, you cannot display the names of files and directories in it by using the ls command, even though search permission on it is turned on.

```
$ chmod 600 sample
$ chmod 500 courses
$ chmod 300 personal
$ ls -ld courses personal sample
dr-x------ 2 sarwar sarwar 512 Aug 4 06:36 courses
d-wx----- 2 sarwar sarwar 62 Aug 4 06:36 personal
drw------ 2 sarwar sarwar 88 Aug 4 06:36 sample
$ mkdir courses/ee345
mkdir: courses/ee345: Permission denied
$ cp foo courses
cp: courses/foo: Permission denied
$ cd sample
cd: sample: Permission denied
$ ls -l personal
total 0
ls: personal: Permission denied
$
```

The next session shows that simply having read or write permission on a directory is not sufficient to read its contents (e.g., display them with the ls command) or create a file or directory in it. For example, the directory dir1 has write permission turned on, but you cannot copy the prog1.cpp file into it, because search permission on it is turned off. Similarly, you cannot remove the file f1 from dir2. After you turn on its search permission with the chmod u+x dir2 command, you can remove the file f1.