sets the i attribute of a file in an ext2 file system. When this attribute is set, the file cannot be modified, deleted, or renamed by anyone. No links can be added to point to this file, either. This attribute can be set or cleared only by the root user. So, you can use this attribute to protect against accidents involving files. When you need to clear the attribute, you can run the following:

```
chattr -i filename
```

A few other interesting features of the ext2 system, such as the undelete attribute, are not yet implemented, but will become available in a future ext2 file system version. If you start using the chattr command, you will notice that you sometimes can't modify or delete a file even though you have permission to do so. This happens when you forget that you had previously set the immutable attribute of the file using chattr; because this attribute does not show up in ls output, it can be confusing. To see which files have what ext2 attributes, run the lsattr program with the filename as the argument.