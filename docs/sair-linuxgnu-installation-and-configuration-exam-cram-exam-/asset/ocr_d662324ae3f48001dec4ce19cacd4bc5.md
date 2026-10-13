Look at the permissions associated with the batterup file again. Because the first number is 7, the owner of this file has read (r), write (w), and execute (x) permission to this file. Because the second number is 6, other users in the owner's group have read (r) and write (w) permissions on this file. Because the third number is 4, everyone else has just read (r) permissions on this file.

Note: A number of commands in this chapter can only be executed by the root or super-user. If you want to experiment with one of these commands, type "su" and enter the root password when prompted.

# umask

When you create a new file or directory, the permissions you get depend on the value of what is known as the umask. Open a command-line interface, and type the umask command. You may get an output like the following:

```
023
```

Before you interpret this number, you need a clear idea of the numeric value of permissions.

For example, if you gave everyone permissions to your files and directories, you would have read, write, and execute permissions for all users. As discussed in the previous section, these permissions correspond to the number 7 (r+w+x = 4+2+1). When applied to all users, they correspond to 777. You could set up the same permissions for all users on the batterup file with the following command:

```
chmod 777 batterup
```

However, the files and directories that you create generally don't have 777 permissions. The permissions that you get depend on the umask value. Type the umask command to find its current value, and then subtract the umask number from 777. If umask=023, then 777-023=754. Consequently, permissions equal 754. When you review the last section and Table 7.3, you can see that 754 corresponds to read, write, and execute permissions for the owner, read and execute permissions for members of the owner's group, and read permissions for all other users.