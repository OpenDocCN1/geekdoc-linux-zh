
way, which is often called **SUID root**. SUID programs are indicated by an s in the owner’s execute bit position in the permission string, as in rwsr-xr-x.

### Set group ID (SGID)

The **set group ID (SGID)** option is similar to the SUID option, but it sets the group of the running program to the group of the file. It’s indicated by an s in the group execute bit position in the permission string, as in rwxr-sr-x. When the SGID bit is set on a directory, new files or subdirectories created in the original directory will inherit the group ownership of the directory, rather than be based on the user’s current default group.

### Sticky bit

The sticky bit has changed meaning during the course of Unix history. In modern Linux implementations (and most modern versions of Unix), it’s used to protect files from being deleted by those who don’t own the files. When this bit is present on a directory, the directory’s files can be deleted only by their owners, the directory’s owner, or root. The sticky bit is indicated by a t in the world execute bit position, as in rwxr-xr-t.

![](img/f339a9f48c4b443e61c74acb4c9c3da4_258_0.png)

These special permission bits all have security implications. SUID and SGID programs (and particularly SUID root programs) are potential security risks. Although some programs must have their SUID bits set to function properly, most don’t, and you shouldn’t set these bits unless you’re certain that doing so is necessary. The sticky bit isn’t dangerous this way, but because it affects who may delete files in a directory, you should consider its effect—or the effect of *not* having it—on directories to which many users should have write access, such as /tmp. Typically, such directories have their sticky bits set.

![](img/f339a9f48c4b443e61c74acb4c9c3da4_258_1.png)

## Using ACLs

Unix-style permissions have served Linux well since its creation and are emphasized on the Linux+ exam; but a new and improved permission system is now available. An **access control list** (ACL) is a list of users or groups and the permissions they’re given. Linux ACLs, like Linux owner, group, and world permissions, consist of three permission bits, one each for read, write, and execute permissions. The file’s owner can assign ACLs to an arbitrary number of users and groups, making ACLs more flexible than Linux permissions, which are limited to groups defined by the system administrator.

ACLs require support in the underlying filesystem. All the major Linux filesystems now support ACLs, but you may need to recompile your kernel (or at least the relevant kernel module) to activate this support.

ACLs require their own commands to set and view. The **setfacl** command sets an ACL, and the **getfacl** command displays the ACLs for a file. Consult these commands’ man pages for more information.

## Changing a File's Mode

You can modify a file’s permissions using the **chmod** command. This command may be issued in many different ways to achieve the same effect. Its basic syntax is as follows:

**chmod _[options]_ [_mode,mode..._] _filename_...**

The **chmod** options are similar to those of **chown** and **chgrp**. In particular, `-recursive` (or -R) changes all the files in a directory tree.

Most of the complexity of **chmod** comes in the specification of the file’s mode. You can specify the mode in two basic forms: as an octal number or as a symbolic mode, which is a set of codes related to the *string* representation of the permissions.

The octal representation of the mode is the same as that described earlier and summarized in Table 4.5. For instance, to change permissions on **report.tex** to *rw-r--r--*, you can issue the following command:

```
$ chmod 644 report.tex
```

In addition, you can precede the three digits for the owner, group, and world permissions with another digit that sets special permissions. Three bits are supported (hence values between 0 and 7): adding 4 sets the set user ID (SUID) bit, adding 2 sets the set group ID (SGID) bit, and adding 1 sets the sticky bit. If you omit the first digit (as in the preceding example), Linux clears all three bits. Using four digits causes the first to be interpreted as the special permissions code.

For instance, suppose you’ve acquired a script called **bigprogram**. You want to set both SUID and SGID bits (6); to make the program readable, writable, and executable by the owner (7); to make it readable and executable by the group (5); and to make it completely inaccessible to all others (0). The following commands illustrate how to do this; note the difference in the mode string before and after executing the **chmod** command:

```
$ ls -l bigprogram
-rw-r--r--    1 rodsmith users    10323 Oct 31 18:58 bigprogram
$ chmod 6750 bigprogram
$ ls -l bigprogram
-rwsr-s---    1 rodsmith users    10323 Oct 31 18:58 bigprogram
```

A symbolic mode, by contrast, consists of three components: a code indicating the permission set you want to modify (the owner, the group, and so on); a symbol indicating whether you want to add, delete, or set the mode equal to the stated value; and a code specifying what the permission should be. Table 4.6 summarizes all these codes. Note that these codes are all case sensitive.

### TABLE 4.6 Codes Used in Symbolic Modes

| Permission Set Code | Meaning | Change Type Code | Meaning | Permission to Modify Code | Meaning |
| :--- | :--- | :--- | :--- | :--- | :--- |
| u | Owner | + | Add | r | Read |
| g | Group | - | Remove | w | Write |
| o | World | = | Set equal to | x | Execute |
| a | All | | | X | Execute only if the file is a directory or already has execute permission |
| | | | | s | SUID or SGID |
| | | | | t | Sticky bit |
| | | | | u | Existing owner's permissions |
| | | | | g | Existing group permissions |
| | | | | o | Existing world permissions |

To use symbolic permission settings, you combine one or more of the codes from the first column of Table 4.6 with one symbol from the third column and one or more codes from the fifth column. You can combine multiple settings by separating them with commas. Table 4.7 provides some examples of chmod using symbolic permission settings.

### TABLE 4.7 Examples of Symbolic Permissions with *chmod*

| Command | Initial Permissions | End Permissions |
| :--- | :--- | :--- |
| `chmod a+x bigprogram` | `rw-r--r--` | `rwxr-xr-x` |
| `chmod ug=rw report.tex` | `r------` | `rw-rw--` |
| `chmod o-rwx bigprogram` | `rwxrwxr-x` | `rwxrwx--` |
| `chmod g=w report.tex` | `rw-r--r--` | `rw-rw-r--` |
| `chmod g-w,o-rw report.tex` | `rw-rw-rw-` | `rw-r-----` |

In Exercise 4.1, you’ll experiment with the effect of Linux ownership and permissions on file accessibility.

## EXERCISE 4.1

### Modifying Ownership and Permissions

During this exercise, you’ll need to use three accounts: root and two user accounts, each in a different group. To study these effects, follow these steps:

1. Log in three times using three virtual terminals: once as root, once as user1, and once as user2. (Use usernames appropriate for your system, though. Be sure that user1 and user2 are in different groups.) If you prefer, instead of using virtual terminals, you can open three xterm windows in an X session, using su to acquire each user’s privileges.
2. As root, create a scratch directory—say, /tmp/scratch. Type `mkdir /tmp/scratch`.
3. As root, give all users read and write access to the scratch directory by typing `chmod 0777 /tmp/scratch`.
4. In the user1 and user2 login sessions, change to the scratch directory by typing `cd /tmp/scratch`.
5. As user1, copy a short text file to the scratch directory using cp, as in `cp /etc/fstab . /testfile`.
6. As user1, set 0644 (rw-r--r--) permissions on the file by typing `chmod 0644 testfile`. Type `ls -l`, and verify that the permission string in the first column matches this value (-rw-r--r--).
7. As user2, try to access the file by typing `cat testfile`. The file should appear on the screen.
8. As user2, try to change the name of the file by typing `mv testfile changedfile`. The system won’t produce any feedback, but if you type `ls`, you’ll see that the file’s name has changed. Note that user2 doesn’t own the file but can rename it because user2 can write to the directory in which the file resides.
9. As user2, try to change the mode of the file by typing `chmod 0600 changedfile`. The system should respond with an **Operation not permitted** error because only the file’s owner may change its permissions.
10. As user2, try to delete the file by typing `rm changedfile`. Depending on your configuration, the system may or may not ask for verification, but it should permit the deletion. This is true despite the fact that user2 doesn’t own the file because user2 can write to the directory in which the file resides.
11. As user1, repeat step 5 to re-create the test file.
