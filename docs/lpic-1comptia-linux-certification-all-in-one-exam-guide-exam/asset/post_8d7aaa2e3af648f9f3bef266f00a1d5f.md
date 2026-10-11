
c. Save your changes and exit the editor.

d. Repeat this process for the rest of your users.

9. Check your new quotas by entering `repquota -av` at the shell prompt. You should now see quotas established for your users.

10. Enter `exit` to leave the root user account.

11. Verify that you are logged in as a user account that quotas have been set for.

12. Create a big file by entering `time dd if=/dev/zero of=bigfile.bin bs=1024 count=10000` at the shell prompt. You should see an error indicating the quota has been exceeded.

You are now an expert at working with Linux users, groups, and permissions!

## Chapter Review

In this chapter, I discussed ownership, permissions, and quotas. I pointed out that users and groups only control who can access the system. They don’t control what the user can do with files or directories in the file system. To do this, I need to implement ownership and permissions.

I pointed out that, whenever a user creates a file or directory, that user is automatically assigned to be its owner. In addition, the group the user belongs to becomes the file or directory’s group owner. These defaults can be changed; however, you must be logged in as root to change a file or directory’s owner or be logged in as its owner to change its group.

To modify ownership, you use the `chown` command. This command can change both the user and/or the group that owns a file or directory. If you only want to change the group, you can also use the `chgrp` command.

I then pointed out that ownership alone can’t control user access to files and directories. To fully control access, I need Linux file system permissions. Permissions define what a user can and cannot do with a given file or directory. Linux uses the following permissions:

- Read
- Write
- Execute

Linux assigns permissions to the following entities:

- Owner
- Group
- Others

The permissions assigned to Owner, Group, and Others together constitute a file or directory’s mode. I also emphasized that Linux permissions are additive. If a given user is both an owner and member of the owning group, then he or she receives permissions assigned for a file or directory to Owner and Group.

I then pointed out that permissions can be represented numerically for Owner, Group, and Others using the following values:

- Read: 4
- Write: 2
- Execute: 1

By adding up each permission assigned to a given entity, you can represent all of the permissions assigned with a single number. For example, a value of 7 indicates that all permissions have been assigned. A value of 5 indicates read and execute permissions have been assigned.

I then discussed the `chmod` tool that is used to manage permissions from the shell prompt. The `chmod` utility can use any of the following syntaxes to assign permissions to Owner, Group, and/or Others:

- `chmod u=rw,g=rw,o=r file_or_directory`
- `chmod u+rw,g+rw,o+r file_or_directory`
- `chmod 664 file_or_directory`

At this point, I began a discussion of default Linux permissions. We pointed out that, by default, Linux automatically assigns new files with `rw-rw-rw-` permissions and new directories with `rwxrwxrwx` permissions upon creation. However, to increase security, the `umask` variable is used to automatically remove some permission. The default `umask` value is 022, which removes the write permission from Group and Others when a file or directory is created. I pointed out that you can change the value of `umask` by entering `umask value` at the shell prompt.

I also briefly discussed the special permissions that you can assign, including:

- SUID: 4
- SGID: 2
- Sticky Bit: 1

I pointed out that you assign these permissions with `chmod` by adding an extra digit before the Owner digit in the command using the values just shown.

I ended the chapter by discussing how to implement disk quotas. I pointed out that disk quotas are used to prevent users from using up too much disk space. To implement quotas, you must first install the quota package on your Linux system. We then reviewed the procedure for setting up quota files for mounted file systems. I pointed out that you can set quotas for the number of blocks a user is allowed to consume (disk space) and/or the number of inodes a user may consume (number of files). For both of these parameters, you can set hard and soft limits. A user may temporarily exceed soft limits for a time you define as the grace period. A user may not exceed a hard limit. You can enter the `repquota -av` command at the shell prompt to view a report displaying hard and soft limits as well as current user space usage.

## Accelerated Review

- Ownership defines which user and group owns a particular file or directory in the file system.
- You can use the `ls -l` command to view ownership.
- You can use the `chown` utility to configure user and group ownership of a file or directory.
- You can use the `chgrp` utility to change group ownership.
- You must be logged in as root to change user ownership.
- You must be logged in as root or as the file/directory owner to change group ownership.
- Permissions are used to define what users may or may not do with files or directories in the file system.
- Linux uses the read, write, and execute permissions for files and directories.
- Linux permissions are assigned to Owner, Group, and Others.
- Linux permissions are additive.
- The permissions assigned to Owner, Group, and Others constitute the file or directory's mode.
- Permissions can be represented numerically: read=4, write=2, and execute=1.
- Summing up all permissions assigned to an entity, such as Owner, allows you to represent all assigned permissions with a single number.
- You use the `chmod` utility to modify permissions.
- Linux assigns `rw-rw-rw-` permissions by default to new files and `rwxrwxrwx` permissions to new directories.
- These permissions are too relaxed for most situations, so the `umask` variable is used to subtract specific permissions from the defaults.
- The default value of `umask` is 022, which subtracts the write permission (2) from Group and Others.
- You can modify the value of `umask` to change the default permissions assigned upon creation.
- Linux also includes three default special permissions: Sticky Bit, SUID, and SGID.
- You assign special permissions with `chmod` by adding an additional digit before the Owner digit in the command.
- You can use the quota package to implement disk quotas in the file system.
- Quotas prevent users from consuming too much disk space.
- You can set quotas for the number of blocks a user is allowed to consume (disk space) and the number of inodes a user may consume (number of files).
- You can set hard and soft limits.
- A user may temporarily exceed soft limits for a time you define as the grace period.
- A user may not exceed a hard limit.
- You can enter the `repquota -av` command at the shell prompt to view a report displaying hard and soft limits as well as current user space usage.

## Questions

1. You need to change the owner of a file named `/var/opt/runme` from mireland, who is a member of the users group, to dnelson, who is a member of the editors group. Assuming you want to change both user and group owners, which command will do this?
   - A. `chown mireland dnelson /var/opt/runme`
   - B. `chown -u "dnelson" -g "editors" /var/opt/runme`
   - C. `chown dnelson /var/opt/runme`
   - D. `chown dnelson.editors /var/opt/runme`

2. Which permission, when applied to a directory in the file system, will allow a user to enter the directory?
   - A. Read
   - B. Write
   - C. Execute
   - D. Access Control

3. A user needs to open a file, edit it, and then save the changes. What permissions does he need to do this? (Choose two.)
   - A. Read
   - B. Write
   - C. Execute
   - D. Modify

4. A file named `employees.odt` has a mode of `rw-r--r--`. If mhuffman is not the file’s owner but is a member of the group that owns this file, what can he do with it?
   - A. He can open the file and view its contents, but he can’t save any changes.
   - B. He can open the file, make changes, and save the file.
   - C. He can change ownership of the file.
   - D. He can run the file if it’s an executable.
