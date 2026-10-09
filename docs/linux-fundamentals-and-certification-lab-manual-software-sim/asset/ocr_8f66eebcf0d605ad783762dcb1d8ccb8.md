![](bbox=[0.03, 0.07, 0.93, 0.22])

available online); just become familiar enough with these options to remember that they are available. Some important basic commands include:

+   * **man**: Formats and displays the online manual pages. Example: `man ls`
* **ls**: List a directory. The option, -l, will give a detailed listing, -F will list the file types, and -a will list hidden files. Example: `ls -la`
* **cd**: Change directory. Example: `cd /etc`
* **mkdir**: Make a directory. Example: `mkdir /home/jsmith/mymusic`
* **rm**: Remove files and directories. To remove a directory, use the -r (recursive) option. To remove a file, type `rm` and then the name of the file. Example: `rm myfi1e` or `rm -r mydir`

* **chmod**: Change file access permissions. (Discussed earlier in this chapter.) `chmod` can use symbolic mode or octal mode. Example: `chmod a+x myfi1e` and `chmod 755 myfi1e` (both give execute permission to all users)

`chown`: Change file owner and/or group. `chown` changes the ownership of a file. This command is most often used when the root user creates a file, then transfers ownership to another user. Anyone with full permissions on a file can change the ownership of the file. The syntax for the command is `chown [option] owner[:group] file`

One useful option is -R, which causes `chown` to act recursively. This means that the ownership can be changed to a directory and all the files within the directory will be changed as well. Suppose that root owns a file called data1 and wants to change ownership to user jsmith in group admin. The command from the directory that data1 is in would be `chown jsmith:admin data1`.

* **chgrp**: Change the group of a file. `chgrp` lets a user change the group ownership of a file. The syntax is similar to the syntax for `chown`:

`chgrp [options] group file`

Suppose that a file named data1 is owned by root, and the root user wants to change group ownership from the root group to the database group. The command from the directory that data1 is in would be `chgrp root database`.

* **mv**: Move a file. Use this command when the file needs to be moved or renamed (renaming a file is the same as moving it). The syntax is `mv [options] source destination` where source is the current file location and destination is where you want it to be relocated.

Suppose that root wants to move the data1 file to jsmith's home directory. The current location of the file is /root. The command to move the file is
`mv /root/data1 /home/jsmith`

If the file needs to be renamed, the new filename can be appended to the end of /home/jsmith. For example, to move data1 and change the name to jsmithdata, use the following:
`mv /root/data1 /home/jsmith/jsmithdata`

If jsmith wants to rename the file within his directory to mydata, he would use the command
`mv jsmithdata mydata`