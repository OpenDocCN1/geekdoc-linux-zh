# # chmod: Changing Permissions

You use the chmod command to change the permission settings of one or more files. The syntax is as follows:

```
chmod [-cfvR] perm files
```

The command changes the permission settings of files to what you specify in the perm argument. The characters within square brackets are the options, and they have the following meanings:

+   - `-c` lists only files whose permissions have changed.
+   - `-f` stops any error message displays.
+   - `-v` verbosely displays permission changes.
+   - `-R` recursively changes permissions of files in all subdirectories.

To use chmod effectively, you have to learn how to specify the permission settings. One way is to concatenate one letter from each column of the following table in the order shown (Who/Action/Permission):

| Who | Action | Permission |
|---|---|---|
| `u` user | `+` add | `r` read |
| `g` group | `-` remove | `w` write |
| `o` others | `=` assign | `x` execute |
| `a` all | `s` set user ID | |

For example, to give everyone read access to all files in a directory, type **chmod a+r ***. On the other hand, to permit everyone to execute a specific file, type **chmod +x filename**.

Another way to specify a permission setting is to use a three-digit sequence of numbers. In a detailed listing of a file that you get when you use the command `ls -l`, the read, write, and execute permission settings for the user, group, and others appear as the sequence `rwxrwxrwx` (with dashes in place of letters for disallowed operations). Think of `rwxrwxrwx` as three occurrences of the string rwx. Now, assign the values:

+   - r = 4
+   - w = 2
+   - x = 1
+   - - = 0