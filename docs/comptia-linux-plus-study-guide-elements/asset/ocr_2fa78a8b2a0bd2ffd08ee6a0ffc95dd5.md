Ordinary users can enter the umask command to change the permissions on new files they create. The superuser can also modify the default setting for all users by modifying a system configuration file. Typically, /etc/profile contains one or more umask commands. Setting the umask in /etc/profile might or might not actually have an effect, because it can be overridden at other points, such as a user's own configuration files. Nonetheless, setting the umask in /etc/profile or other system files can be a useful procedure if you want to change the default system policy. Most Linux distributions use a default umask of 002 or 022.

To find what the current umask is, type umask alone, without any parameters. Typing umask -S displays the umask expressed symbolically, rather than in octal form. You may also specify a umask in this way when you want to change it, but in this case, you specify the bits that you do want set. For instance, typing umask u=rwx,g=rx,o=rx is equivalent to typing umask 022.

# Using ACLs

The Unix file permission system used by Linux was designed long ago. As frequently happens, real-world needs highlight limitations in early designs, and this is true of Unix permissions. For instance, using Unix permissions to provide fine-grained access control on a user-by-user basis is difficult or impossible. That is, if you want to enable the users amy, david, theo, and lolo to read a file, but no other users, you must create a group that holds just those four users and no others, assign group ownership of the file to that group, and set group and world permissions appropriately. If you want only amy and david to be able to read another file, you must repeat this process, creating another group. What's more, because only root can ordinarily create groups, users have little control over these matters.

A more flexible approach is to use access control lists (ACLs). These are permissions that can be assigned on a user-by-user basis. For instance, you can create ACLs allowing amy and david to access a file without creating or modifying any groups. In Linux, ACLs can provide separate read, write, and execute access; they are effectively an extension of the normal Unix-style permissions.

One problem with ACLs is that they're not yet universally supported. The filesystem you use must support ACLs. In modern Linux kernels, the ext2fs, ext3fs, ext4fs, ReiserFS, JFS, and XFS filesystems all support ACLs. This support may not be present in more obscure filesystems or in older kernels, though. ACL support is optional with all of the filesystems that support it; it must be enabled when the kernel is compiled, and this isn't always done.

Assuming your Linux filesystem supports ACLs, both root and ordinary users may create ACLs using the setfacl command:

```
```
setfacl [options] [(-m | -x) acl_spec] [(-M | -X) acl_file] file
```
```

The -m and -M parameters set an ACL, while the -x and -X parameters remove an ACL. The uppercase variants take an ACL out of a file, whereas the lowercase variants require you to enter the ACL on the command line. The ACL format itself takes this form:

*scope*:ID:*perms*