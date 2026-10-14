# 5.4 Setting File and Directory Permissions (chmod)

Your ability to change permissions gives you a great deal of control over the way your data can be used. Use the chmod (change mode) command to set or change the permissions for your files and directories.

For example, you obviously permit yourself to read, modify, and execute a file. You generally permit members of your group to read a file. Depending upon the nature of your work and the composition of your group, you often let them modify or execute it. You generally prohibit all other system users from having any access to a file.

> Note
> 
> You must be the owner of the file or directory (or have superuser authority) before you can change its permissions. This means that your user name must be in the third field in an ls -l listing of that file.

It is important to realize that whatever restrictions you impose on file and directory access, the superuser can always override them. For example, if you use the chmod command to specify that only you can have access to the report20 file, the superuser can still access this file. For more information on this topic, see Section 5.7.

There are two ways to specify the permissions set by the chmod command:

+   - You can specify permissions with letters and operation symbols.
+   - You can specify permissions with octal numbers.

The following sections describe how to specify permissions with letters and operation symbols, as well as with octal numbers.

# 5.4.1 Specifying Permissions with Letters and Operation Symbols

You can use letters and operation symbols to change file and directory permissions.

The following is the format of the chmod command when using letters and operation symbols:

```
chmod userclass-operation-permission filename
```

The userclass-operation-permission entry actually represents three codes that specify the user class, group, operation, and permission code that you want to activate. The filename entry is the name of the file or files whose permissions you want to change. You may also use pattern-matching characters to specify files. See Section 5.4.1.3 for more information.