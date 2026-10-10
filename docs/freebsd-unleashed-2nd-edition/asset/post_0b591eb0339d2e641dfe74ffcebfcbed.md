
- 2–Set group ID (setgid). If this bit is set on an executable file, it will be executed with the effective group permissions of the file's group owner rather than those of the user executing it. A file can only be made setgid by the super-user.
- 4–Set user ID (setuid). If this bit is set on an executable file, it will be executed with the effective user permissions of the file's user owner rather than those of the user executing it. A file can only be made setuid by the super-user.

This fourth digit is the highest-value digit (in other words, the leftmost one), so in the earlier example where we showed what the permissions of 755 mean, we could have used the equivalent value 0755. We use the same method to construct the value for that digit as we do for the other digits, so the value 3755 would create a directory with the sticky bit and the setgid bit set, in addition to the regular 755 permissions.

## Changing Modes Symbolically

As clever as the octal numeric system is, it’s helpful to have a method for setting modes that’s easier to remember. Fortunately, we have a symbolic method for doing just that.

Instead of giving `chmod` a number, you can give it between one and three flags in a single string. This string can be formatted in a number of ways, but we’ll briefly cover the most common usages here.

> **NOTE**  
> See `man chmod` for complete coverage of the flexible syntax of `chmod` and its symbolic modes.

Table 9.4 shows some examples of symbolic modes. Each is made up of a string of characters. The first character specifies the ownership mode(s), the second character indicates the modification you’re making (+, -, or =), and the third is the permission bit(s).

| Mode String | Meaning |
| :--- | :--- |
| go+w | Adds “write” permissions to the group owner and others |
| +x | Adds “execute” permissions for everyone |
| o-r | Removes “read” permissions for others |
| ugo=rw | Sets “read” and “write” permissions for everyone |
| a=rw | Same as ugo=rw |
| +t | Adds the sticky bit (super-user only) |
| +s | Adds both the setuid and setgid bits (super-user only) |

To set the file `file.txt` so that it is “group writable,” use the following command:
```
# chmod g+w file.txt
```

This symbolic method lends itself more readily to memory than the numeric method, and it will probably be a much easier way for you to perform most of your typical `chmod` operations.

> **TIP**  
> The `-R` option works on `chmod`, too, the same as with `chown` and `chgrp`.

## Access Control Lists (ACLs)

The Access Control List (ACL) is a new addition to FreeBSD 5.0 that gives you tighter control over who can and cannot access files and directories. Instead of just allowing or denying access based on owner, group, and everyone else, you can now grant access to individual users and individual groups. You can also set a maximum permission mask for the users and groups that are granted access through an ACL that will override the actual permissions given by the ACL.

For an ACL to work, UFS Extensions must be compiled into the kernel. The next section explains the options that must be added.

### Configuring the Kernel to Support ACL

At the time of this writing, it is not known for sure whether UFS Extensions will be enabled in the default kernel for the release of version 5.0. If they are enabled, you do not need to rebuild the kernel. If they are not, you will need to add the UFS Extension options to the kernel configuration file and then rebuild the kernel.

To see whether your kernel has UFS Extensions enabled, look for the following lines in your kernel configuration file. Unless you have already built a custom kernel, your kernel configuration file will be `/usr/src/sys/i386/conf/GENERIC` on an Intel x86-based system and `/usr/src/sys/alpha/conf/GENERIC` on an Alpha-based system. The following lines should be present in order for an ACL to work:

```
options   UFS_EXTATTR
options   UFS_EXTATTR_AUTOSTART
options   UFS_ACL
```

If these options are already present in your kernel configuration file, you don't need to do anything. If they are not present, you will need to add these options and then build a new kernel. See Chapter 16, "Kernel Configuration," for full details on how to configure, build, and install a new kernel.

> **TIP**  
> Further documentation on the kernel modifications necessary for ACLs can be found in the source tree, in the `README.*` files in `/sys/ufs/ufs`.

After you have installed the new kernel and rebooted, you will need to configure the filesystems you want to use the ACL with.

### Configuring Filesystems to Use ACLs

The `extattrctl` command is used to control the extended attributes on filesystems. You must use it on each filesystem you want to use an ACL with. For example, to enable an ACL on the filesystem mounted as `/usr`, follow this procedure:

> **CAUTION**  
> The files created by the commands in the ACL-enabling process can be extremely large, possibly taking up several gigabytes of disk space on large filesystems. Make sure you have plenty of free disk space before running the commands.

1. As the root user, create the directories `/usr/.attribute` and `/usr/.attribute/system`:
   ```
   # mkdir /usr/.attribute /usr/.attribute/system
   ```
2. Change to the newly created `/usr/.attribute/system` directory (`cd /usr/.attribute/system`) and then run the `extattrctl` command to initialize the ACL attributes on the filesystem:
   ```
   # extattrctl initattr -p /usr 388 posix1e.acl_access
   ```
   On large filesystems, this command can take several minutes to complete, so be patient as the command generates the backing files needed to support the ACL.
3. When the first command has finished executing, run the `extattrctl` command one more time with a different filename as the argument:
   ```
   # extattrctl initattr -p /usr 388 posix1e.acl_default
   ```
   Once again, on a large filesystem, this command can take several minutes to complete, so be patient.
4. Reboot the system or remount the filesystems in question for the changes to take effect. After you have done so, the ACLs for the filesystem will be enabled.

### Getting Information About Current ACL Settings

Use the `getfacl` command to obtain information about existing ACL settings on files or directories. For example, on a newly created file named `acltest.txt` with no ACL set and with default 644 permissions, issuing `getfacl acltest.txt` will return the following:

```
#file:acltest.txt
  #owner:0
  #group:0
  user::rw-
  group::r--
  other::---
```

The first line simply shows the name of the file. The next two lines show the UID and GID, respectively, of the owner and group the file belongs to (in this case, the file is owned by root). The final three lines show the current file permissions on the file. Notice that “other” does not have any permissions on this file.

### Setting the Maximum Permissions Mask

The maximum permissions mask controls the maximum permissions that will be given to any user or group added to the ACL list. Note that the mask applies only to users and groups that are given access to the file or directory with an ACL entry; the mask doesn’t affect the owner’s permissions. It also does not affect the permissions that the default group has, nor does it affect the permissions of the rest of the world. For anyone not listed in an ACL entry, the standard file access permissions apply.

The `setfacl` command is used to add, modify, or delete entries from the ACL list. The syntax is
```
# setfacl action permissions filename
```
where `action` is the action that should be performed (adding an entry, modifying an entry, deleting an entry, and so on), `permissions` is the ACL permissions that should be set, and `filename` is, of course, the name of the file or directory that the ACL should be applied to. The following example adds an ACL maximum permissions mask of read to the file `acltest.txt`:

```
setfacl -m::r acltest.txt
getfacl acltest.txt
#file:acltest.txt
#owner:0
#group:0
user::rw-
group::r--
mask::r--
other::---
```

In the `setfacl` command, the `-m` option means that you want to add or modify the ACL entry. The `m::` specifies that you want to set a mask, and the `r` simply means “read.” If you want to also set the mask to allow write permissions, you would use `m::rw`. The last entry is, of course, the name of the file you want this operation to be performed on.
