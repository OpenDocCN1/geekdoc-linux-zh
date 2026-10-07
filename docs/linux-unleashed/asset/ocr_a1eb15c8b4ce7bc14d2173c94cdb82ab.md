# # The su Command

Sometimes you want to execute a command as another user. If you are logged in as superuser and want to create files with bill's permissions and ownership set, it is easier to log in as bill than work as root and then reset all the parameters. Similarly, if you are logged in as a user and need to be superuser for a little while, you would have to log out and back in to make the change. An alternative is the su command.

The su command changes your effective username and grants you the permissions that username has. The su command takes the username you want to change to as an argument. For example, if you are logged in as a typical user and want to be root, you can issue the following command:

```
su root
```

The Linux system prompts you for the root password. If you supply it correctly, you will be root until you issue a Ctrl+D to log out of that account and back to where you started. Similarly, if you are logged in as root and want to be a user, you can issue the command with the username, such as the following:

```
su tparker
```

You won't be prompted for a password when changing from root to another user because you have superuser powers. When you Ctrl+D out of the login, you are back as root. If you are logged in as a normal user and want to switch to another non-root login, you have to supply the password, though.

# # Summary

In this chapter we've looked at the basics of the /etc/passwd and /etc/group files, the two files intimately connected with user access to Linux. As you have seen, these are simple files and can easily be modified by a system administrator to add users and groups at any time. Always bear in mind that these are vital files, and they should be copied to a backup filename, then edited carefully and their permissions checked after each edit. From here, you can explore the following topics:

+   - Learn more about SCSI (Small Computer System Interface) devices and how they add to your Linux system’s flexibility in Chapter 36, “SCSI Device Support.”
- Learn more about setting up e-mail on your Linux system in Chapter 40, “Configuring Linux for Mail.”
- Learn more about the tar command, backups, and the importance of making back-up copies of your system in Chapter 45, “Backups.”