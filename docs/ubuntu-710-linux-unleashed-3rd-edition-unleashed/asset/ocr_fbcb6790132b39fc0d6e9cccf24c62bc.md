```
- > /usr/share/example-content

-rw-r--r--  1 root root  566 2007-05-17 12:59 .profile
```

Each line provides the file permissions, the number of files housed under that file or directory name, the file owner, the file group, the file size, the creation date, and the filename.

As you can see, root owns every file here, but the adduser command (a symbolic link to the actual command named useradd) copies everything in /etc/skel to the new home directory and resets file ownership and permissions to the new user.

Certain user files might exist that the system administrator doesn't want the user to change; the permissions for those files in /home/username can be reset so that the user can read them but can't write to them.

userdel—This command completely removes a user's account (thereby eliminating that user's home directory and all files it contains).

passwd—This command updates the "authentication tokens" used by the password management system.

# TIP

To lock a user out of his account, use the following command:

```
$ sudo passwd -l username
```

This prepends an ! (exclamation point, also called a bang) to the user's encrypted password; the command to reverse the process uses the -u option. This is a more elegant and preferred solution to the problem than the traditional UNIX way of manually editing the file.

usermod—This command changes several user attributes. The most commonly used arguments are -s to change the shell and -u to change the UID. No changes can be made while the user is logged in or running a process.

chsh—This command changes the user's default shell. For Ubuntu, the default shell is /bin/bash, known as the Bash, or Bourne Again Shell.

# Adding New Users

The command-line approach to adding this user is actually quite simple and can be accomplished on a single line. In the example shown here, the sysadmin uses the useradd command to add the new user bernice. The command adduser (a variant found on some UNIX systems) is a symbolic link to useradd, so both commands work the same. In this example, we use the -p option to set the password the user requested; we use the -s to set