# # Managing Users and Groups from the Command Line

Although **Linuxconf** gives you the option of having a GUI admin tool for managing users and groups, you can also manage users and groups from the command line. This is something Linux is pretty famous for.

# ## Adding Users

The **useradd** command is a command-line utility that you can use to create a new user or to update an existing user. To add new user Barney Rubble to the system, simply su to root and type:

```
[root@cartoons]# useradd -c "Barney Rubble" -d /home/brubble brubble
```

![](bbox=[0.06, 0.42, 0.85, 0.5])

The `-c` option is the full name of the person. The `-d` option is the home directory that you would want to create for this new user. Lastly, you specify the userid of your new user. Now you can assign a password to the user ID:

```
[root@cartons]# passwd brubble
Changing password for user brubble
New UNIX password:
```

You could have set the password by including the `-p` option in the **useradd** command, but it requires the encrypted password. The two-step process is a little easier if you are manually creating a new user.

For a more detailed listing of available options for these commands, you can view the man pages for **useradd**.

# ## Changing User Passwords

The user **root** can use the **passwd** command to change the password for any user. If you would like to change the password for the current user logged in, yourself, type **passwd**. For obvious reasons, the system will prompt you for your current password before it assigns you a new one.