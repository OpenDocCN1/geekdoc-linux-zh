
## Controlling Access to Files

Read and write permissions for the owner. Read-only permission for all others.

Read and write permissions for the owner, and read-only permission for the group. No permission for others.

Read and write permissions for the owner. No permission for anybody else.

Read permission for the owner. No permission for anybody else.

Execution permissions makes sense for ordinary files, but it's meaningless for most other file types, directories, though, the execute bit another way. When a directory's execute bit is set, it means that the directory's contents may be searched. This is a highly desirable characteristic for directories, so you'll almost never find a directory on which the execute bit is set in conjunction with the read bit.

Directories can be confusing with respect to permission. Recall that directories are interpreted in a special way. As such, if a user can write to a directory, they can create, delete, or rename files in the directory, even if the user isn't the owner of those files and does not have permission to write to those files. You can use the sticky bit (described shortly, in "Special Permissions") to alter this behavior.

Symbolic links are unusual with respect to permissions. This file type always has 777 (rwxrwxrwx) permissions, granting all users access to it. This access applies only to the link itself, not to the linked-file. In other words, all users can read the contents of the link to discover the name of the file to which it points, but the permissions on the linked-file determine its access. Changing the permissions on a symbolic link affects the linked-file.

Many of the permissions don't apply to root. The superuser can read or write any file on the computer—even files that grant access to nobody (that is, those that have 000 permissions). The superuser still needs execute bit to run a program file, but the superuser has the power to change the permissions on any file, so this limitation is not very substantial. Some files may be inaccessible to root, but only because of an underlying restriction—even root can't access a disk that isn't installed in the computer.

## Special Permission Bits

A few permission options are also supported, and they may be indicated by changes to the permission string:

- **Set User ID (SUID)**: The set user ID (SUID) option is used in conjunction with executable files, and it lets Linux to run the program with the permissions of whoever owns the file rather than with the permissions of the user who runs the program. For instance, if a file is owned by root and has its UID bit set, the program runs with root privileges and can read any file on the computer. Some servers and other system programs run this, which is often called SUID. SUID programs are indicated by an s in the owner's execute position in the permission string, as in `rwsr-xr-x`.

- **Set Group ID (SGID)**: The *set group ID* (SGID) option is similar to the SUID option, but it sets the group of the running program to the group of the file. It is indicated by an s in the group execute position in the permission string, as in `rwxrsr-x`. When the SGID is set a directory, new files or subdirectories created in the original directory inherit the group ownership of the directory, than based on the user's current default group.

- **Sticky Bit**: The sticky bit has changed meaning during the course of Unix. In modern Linux implementations (and most modern versions of Unix), it's used to protect files from being deleted by those who do not own them. When this bit is present on a directory, direct's files can be deleted only by their owners, the directory's owner, or root. The sticky bit is indicated by a t in the world execute position, as in `rwxrwt`.

These special permissions all have security implications. SUID and SGID programs (particularly SUUID root programs) are security risks. Although some programs must have SUID bits set properly, some don't, and you shouldn't set these bits unless you're certain that doing so is necessary. The sticky bit is not dangerous this way, because it affects the effect of not having it—on directories to which many users should have write access, as /tmp. Typically, directories have their sticky bits set.

![](img/35f616c7eba4e79e12bfd762129c5d27_252_0.png)

## Using ACLs

Unix-style permissions have served Linux well since its creation and are emphasized on them. An *access control list (ACL)* is a list of users or groups and the permissions they're given. Linux ACLs, like Linux owner, group, and world permissions, consist of three permission bits, one each for read, write, and execute permissions. The file's owner can assign ACLs to *any arbitrary* number of users and groups, making ACLs more flexible than Linux permissions, which are limited to defined groups by the system administrator.

ACLs require support in the underlying filesystem. All the major Linux systems now support ACLs, but you may need to recompile your kernel (or at least the relevant kernel module) to activate this support.

ACLs require their own commands to set and view. The `setfacl` command sets an ACL, and the `getfacl` command displays the ACLs for a file. Consult these commands' man pages for more information.

## Changing a File's Mode

You can modify a file's permissions using the chmod command. This command may be issued in many ways to achieve the same effect. Its basic syntax follows:

`chmod [options] [mode,...] filename`

The chmod options are similar to chown and chgrp. In particular, --recursive (-R) changes all files in the. Most of the complexity of chmod comes in the specification of the mode. You can specify the mode in two forms: as an octal number or as symbolic mode.

A symbolic mode, by contrast, consists of three components: a code indicating the permission you want to modify (the owner, the group, and so on); a symbol indicating whether you want to add, delete, or set the mode equal to; and a code specifying what the permission should be. Table 4.6 summarizes all these codes. Note that these codes are all case-sensitive.

### TABLE 4.6 Codes used in symbolic modes

| Permission set code | Meaning | Change type code | Meaning | Permission to modify | Meaning |
| :--- | :--- | :--- | :--- | :--- | :--- |
| u | Owner | + | Add | r | Read |
| g | Group | - | Remove | w | Write |
| o | World | = | Set equal to | x | Execute |
| a | All | | | X | Execute only if the file is a directory or already has permission |
| | | | | s | SUID or SGID |
| | | | | t | Sticky bit |
| | | | | u | Existing owner's permissions |
| | | | | g | Existing group permissions |
| | | | | o | Existing world permissions |

To use symbolic permission settings, you combine one or more of the codes from the first column of Table 4.6 with one symbol from the third column and one or more codes from the fifth column. You can combine multiple sets by separating them with commas. Table 4.7 provides some examples of chmod using symbolic permission settings.

### TABLE 4.7 Examples of symbolic permissions with chmod

| Command | Initial permissions | End permissions |
| :--- | :--- | :--- |
| chmod a+x bigprogram | rw-r--r-- | rwx-xr-x |
| chmod ug=rw report.tex | r--------- | rw------- |
| chmod o-rwx bigprogram | rw-rwx-X | rw-rwx--- |
| chmod g=u report.tex | rw-r--r-- | rw-r-- |
| chmod g-w,o-rw report.tex | rw-rw-rw- | rw------- |
