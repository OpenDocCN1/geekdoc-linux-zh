
```
>ls -l

-rwxr--r-- 1 jray jray 2024 Oct 28 20:39 kiwi.tar

-rw------- 1 jray test 1463882 Jul 2 11:33 magical-beans.gz

drwxrwxr-x 5 jray test 1024 Nov 5 12:25 kytn

...
```

## Listing Owners and Groups

Some versions of `ls` won't show you the owner and group simultaneously with this command. Usually, they list group and owner if you add the `-g` option, as in `ls -lg`.

The information you're interested in here is in the first, third, and fourth columns:

- The first column identifies the owner, group, and world permissions that are active for a file or directory. The first character is a `d` if the filetype is a directory. Normally this is a `-` for a normal file. The remainder of the characters, as you might guess, stand for read, write, and execute (`x`). The first three characters (following the initial `-` or `d` character) are the active owner permissions, the second three characters are the group permissions, and the last three are world permissions.
- The third column is the file owner.
- The fourth column is the group owner.

In this example, the `kiwi.tar` file has read/write permissions for the owner, and read permissions active for the group and world. The owner of the file is `jray` and the group that the file belongs to is `jray`. The second file, `magical-beans.gz`, only has read/write permissions for the owner. (`jray`). The group that `magical-beans.gz` belongs to is `test`; the group `test` has no permissions to operate on the file. The last "file," `kytn`, is actually a directory. The owner of `kytn` is `jray` and the corresponding group is `test`. The owner and group both have full read, write, and execute permissions for this directory, whereas the world has only read and execute.

### CHANGING PERMISSIONS: chmod

Now that you know what permissions are, you probably want to know how to change them. This is accomplished with the `chmod` command. There are two modes of operation that you can use with `chmod`: a quick-and-dirty mode, and a more user-friendly method of setting permissions.

The symbolic user-friendly mode uses easy-to-remember commands to set or unset permissions. To use this, do the following:

1. Pick a permission level. If you want to set permissions for the owner, the level is `u`. If you want to change permissions for the group, it is `g`. For world permissions, choose `o`. Lastly, if you want to affect all the levels of permissions (owner, group, and world), use `a`.
2. Choose an operation. Decide whether you want to set (turn on) or unset (turn off) a particular level of permission. If you want to set a permission, the operation is `+`; if you want to unset a permission, it is `-`.
3. Choose the permission itself. If you want to operate on the read permission, choose `r`, for write choose `w`, and for execute choose `x`.
4. Issue the `chmod` command in this manner: `chmod <permission level><operation><permission> <filename> <filename> ...`

For example, if you want to activate group write permissions for the “`magical-beans.gz`” file shown earlier, type the following:

```
>ls -l magical-beans.gz

>chmod g+w magical-beans.gz
```

To see if this worked, you can run `ls -l` on the filename as follows:

```
>ls -l magical-beans.gz

-rw--w--- 1 jray test 1463882 Jul 2 11:33 magical-beans.gz
```

Sure enough, write permissions are now active for the `test` group members.

Because of its symbolic nature, this method for adjusting file permissions might be easy for some; however, there is another syntax that you might find faster and easier. This deals with setting the actual bit mask that controls a file's permissions. Turning on one of three binary bits can represent each level of permissions. The first of these bits (from left to right) controls read, the second controls write, and the third toggles execute.

Look at it this way:

```
100 - Read permission - The decimal equivalent of
this binary value is 4.

010 - Write permission - The decimal value for write is 2.

001 - Execute permission - The decimal representation is 1.
```
