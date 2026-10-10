the `-i` option, which interactively prompts the user to choose whether to continue with the deletion. Like the `cp` and `mv` commands, the `rm` command accepts the `-f` option to override this choice and immediately delete the file. An example demonstrating the use of the `rm` and `rm -f` commands to remove the current and `hosts2` files is shown here:

```
[root@server1 ~]# ls -f
Current@ Desktop/ hosts2 myprogram* myscript2* proj_files/
[root@server1 ~]# rm current
rm: remove 'current'? y
[root@server1 ~]# rm -f hosts2
[root@server1 ~]# ls -f
Desktop/ myprogram* myscript2* proj_files/
[root@server1 ~]# _
```

To remove a directory, you can use the **rmdir (remove directory)** command; however, the `rmdir` command only removes a directory if it contains no files. To remove a directory and the files inside, you must use the `rm` command and specify that a directory full of files should be removed. As explained earlier in this chapter, you need to use the recursive option (`-r`) with the `cp` command to copy directories; to remove a directory full of files, you can also use a recursive option (`-r`) with the `rm` command. If, for example, the root user wants to remove the `proj_files` subdirectory and all of the files within it without being prompted to confirm each file deletion, the command she must use is `rm -rf proj_files`, as shown in the following example:

```
[root@server1 ~]# ls -f
Desktop/ myprogram* myscript2* proj_files/
[root@server1 ~]# rmdir proj_files
rmdir: 'proj_files': Directory not empty
[root@server1 ~]# rm -rf proj_files
[root@server1 ~]# ls -f
Desktop/ myprogram* myscript2*
[root@server1 ~]# _
```

![](bbox=[0.16, 0.64, 0.27, 0.72])

> In many commands, such as `rm` and `cp`, both the `-r` and the `-R` options have the same meaning (recursive).

![](bbox=[0.16, 0.74, 0.27, 0.83])

> The `-R` option to the `rm` command is dangerous if you are not certain which files exist in the directory to be deleted recursively. As a result, the `-R` option to the `rm` command is commonly referred to as the *résumé* option; if you use it incorrectly in a production server environment, you might need to prepare your résumé.

It is important to note that the aforementioned file management commands are commonly used by Linux users, developers, and administrators alike. Table 4-2 shows a summary of these common file management commands.