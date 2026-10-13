6. Assign a new password with the `passwd tr` command. Once complete, user tr can assign a new password to himself with the same command.

7. Copy basic initialization files, which are normally stored in the `/etc/skel` directory. These are the files, such as `.bashrc` and `.bash_profile`, covered in Chapter 6. Change your identity to the new user with the `su - tr` command. Copy these files with the `cp /etc/skel/.* /home/tr` command.

8. Log out, and tell your new user about his new username and password.

> Note: The steps are slightly different if you have encrypted passwords in a `/etc/shadow` file. Details of this process are not covered on this Sair Installation and Configuration exam.

# adduser

When you're working with a large number of users, you need a method that can help you add users quickly. One way of automating the user creation process is to use the adduser command. To use the adduser command to set up tr's account, type the following:

```
adduser tr
```

Depending on your distribution, this command may prompt you for other settings, such as group and password. Alternately, it may take settings from the control file `/etc/adduser.conf`. In some distributions, the adduser command works just like the useradd command.

# useradd

You can also use the useradd command to create a new user. To use the useradd command to set up tr's account, type the following:

```
useradd tr
```

# userdel

The userdel command is also straightforward. If you have a user named Theodore Roosevelt who just left your company, you'll want to deactivate his account. Once you've retrieved any files you need from his home directory, run the following command:

```
userdel -r tr
```