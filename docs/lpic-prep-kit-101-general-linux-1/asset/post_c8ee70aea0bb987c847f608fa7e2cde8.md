
When determining access to a directory, permissions are a little different. If the permission block on a directory is

```
rwxr--x-r-x
```

then the owner of the directory can read the contents of this directory, create new files and directories in this directory, and make this directory his working directory.

The group members and everyone else can read the directory's contents and make the directory their working directory. However, these people cannot create new files or directories within this directory. Their ability to change an existing file are determined by the permissions defined on that file.

## Key Concept

When evaluating permissions applied to a directory, you need the read permission to list the contents of the directory, the write permission to create or delete files in that directory, and the execute permission to make that directory your working directory.

## Changing Permissions

To change permissions on a file or directory, use the **chmod** command. Only the owner or superuser (root) can change the permissions on a file or directory. Two ways to use this command are by symbols and by numbers. You will see questions that cover changing permissions using both methods, so be familiar with them.

### Changing Permissions with Symbols

The syntax to use symbols is

```
chmod <who> <change> <right> [files]
```

The **who** refers to whether you want to change the permissions for the owner, the group, or everyone. These are represented by the letters *u* (owner), *g* (group), *o* (others), and *a* (all). More than one *who* can be specified. If the *who* is omitted, *a* (all) is assumed and the changes are applied to the owner, the group, and everyone else.

The *change* refers to whether you want to grant or deny a permission—use **+** to grant it or **-** to deny it. The permissions are *r* (read), *w* (write), and *x* (execute). You also must specify the file or directory that will get the new permissions.

Any permissions that already might have been granted will not be changed. If you are granting the group the write permission, as in

```
chmod g+w filename
```

and they already have the read permission, the group’s permission block would be rw-, not just -w-.

You also can explicitly set permissions by using the = operator, which will replace any existing permissions. So, look again at the last example where the group has read permission but you want them to have write permission. If you type

```
chmod g=w filename
```

the new permission block would be -w-, and not rw-. When using the = change operator, all old permissions are gone and only those you specify will be granted.

The who, change, and permission arguments must not have any spaces between them. Also, multiple selections can be used in a single command. For example

```
chmod ug+x MyFile
```

would add the execute permission for the owner and the group. If the permission block on MyFile was rwxrw-r--; before the change, after the change it would be rwxrwxr--.

However, if you typed

```
chmod ug-x MyFile
```

the new permissions would be --x-xrx--. Notice that any who that is not specified is not changed. In this example, others had the read permission before and after the change because others were not mentioned when using the chmod command.

If you do not follow the = with a permission, all permissions for the who are removed. For example, if you have a file with a permission block of -rwxrwxrwx and enter

```
chmod go- filename
```

the new permission block would be -rwxr--r--. Notice that the permissions for both group and others have been removed.

Because using the - operator revokes any previous permissions, it is important to be careful when using - to set permissions. On the other hand, setting explicit permissions gives you more power to ensure that permissions are set exactly like you want them to be.

For example, say you type the following:

```
chmod go-x MyFile
```

This removes the execute permission from both the group and others. If the group and others did not have the execute permission to begin with, no changes would be made. However, if the permission to execute `MyFile` had been previously granted to one or the other, it would be removed but the status of the read or write permission would be unchanged.

**Key Concept**

> When using symbols to change permissions, only those specified permissions and those specified for the *who* are changed unless you use the equal sign (=).

You also can use wildcards when referencing files, such as

```
chmod go+rW letter*
```

This command grants read and write permissions to the owner and group to any file beginning with `letter`. If you want to grant full access to a file, type the following:

```
chmod +rwx memo*
```

This command gives read, write, and execute permissions to the owner, group, and others to any file beginning with `memo`. This will not work, however, if there are any files beginning with `memo` that you do not own. You will get an error message from `chmod`:

```
chmod: file3: Operation not permitted
```

This identifies the file in which the permissions were not changed.

A shortcut to granting permissions is to grant them based on another set of permissions. If you had a file with a permission block of `-rwxr-xr--` and you wanted anyone to be able to execute the file, you could issue the command

```
chmod o=g MyFile
```

which would set the others' permissions to the same as the group or `-rwrx-r-x`. Remember, if you use this method you are setting the permissions explicitly. In other words, the existing permissions for others are erased and then set to mirror the permissions set for group.

You can use any of the three *whos* to set equal permissions by using *u* for owner, *g* for group, and *o* for all others.

If you want to change the permissions for all files and subdirectories, use `chmod` with the `-R` option. This will force `chmod` to recursive down through the directory structure and change all the permissions. Other options to use with the `chmod` command are listed in Table 9.3.

**Table 9.3 Options to Use with chmod**

| Option | Action |
| :----- | :----- |
| -c     | Displays the names of those files whose permissions are changed |
| -f     | Does not display any error messages |
| -v     | Displays a list of each file that is changed and any error messages |

## Changing Permissions with Numbers

You can change permissions by passing a three-digit octal number to the `chmod` command. This octal number represents the bit pattern for the new permissions. Each digit of this number represents the permissions for one of the entities—owner, group, and others, in that order. See Figure 9.3.

![](img/8dd1e68596303df43cb8ccf3197e8e53_235_0.png)

**Figure 9.3**

Setting permissions using an octal number with the `chmod` command.

The value of each permission is shown in Table 9.4.

**Table 9.4 Numbers Used to Grant Permissions**

| Number | Permission |
| :----- | :----- |
| 4      | Read (r) |
| 2      | Write (w) |
| 1      | Execute (x) |

You sum the permissions you want to grant and pass that number to `chmod`. If you enter the command

```
chmod 764 MyFile
```

you would be granting read, write, and execute to the owner, which is 4 (read) + 2 (write) + 1 (execute) = 7. The group is granted read and write, or 4 (read) + 2 (write) = 6. And all others would get read only, or 4.

When you use chmod with numbers you are setting explicit permissions. Any existing permissions on the file or directory are erased and the newly defined permissions are applied—so be careful.

## Special Permissions

Now that you know how to change permissions, you need to know how to use them in some special circumstances. You should give careful consideration to your decision to use these special permissions.

These permissions can be set either by using symbols or by adding a fourth digit when using numbers. This digit goes before the three digits used to set permissions. You can expect to see questions covering these permissions just like setting the read, write, and execute permissions.

### SUID and GUID

The first permission is set user ID (SUID) or set group ID (SGID). This permission changes the user’s ID to that of the who parameter when setting the permission during file execution. This permission is represented as s, which appears instead of x.

If you have a file called *MyFile* with a permission block of ·rwxr·xr·x and you issue the command

```
chmod o+s MyScript
```

then whenever anyone executes the file *MyScript* they will have the same privileges as if they were the owner running that file. Now, if you examined the permission block for *MyScript*, you would see ·rwsr·xr·x. You could accomplish the same thing by using numbers with the `chmod` command:

```
chmod 4755
```

Table 9.5 shows the numbers that can be used before the three digits used to set permissions and their effects.

**Table 9.5 Interpreting the First Digit When Using a Four-Digit Octal Number to Set Permissions**

| Digit | Meaning |
| :--- | :--- |
| 4 | Sets user ID when executing program |
| 2 | Sets group ID when executing program |
| 1 | Sticky bit |
