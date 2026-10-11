Users can use the `-1` option to view their own information, or the root user can view another user's information with this option:

```
chage -1 snuffy
```

This produces the following output:

```
Maximum:           0
Minimum:           99999
Warning:           7
Inactive:         -1
Last Change:       Mar 19, 2004
Password Expires:  Never
Password Inactive: Never
Account Expires:   Never
```

The `passwd` utility includes some of the previous options, such as these:

+   - **\_d**—Disables a user account by removing its password.

+   - **\_n**—Sets the minimum password lifetime in days.

+   - **\_x**—Sets the maximum password lifetime in days.

+   - **\_w**—Sets the warning number of days before the password expires.

+   - **\_i**—Sets the number of days an account with an expired password can be inactive before it's locked.

+   - **\_s**—Shows the user password information, such as what encryption is used and whether a password is set. This does not support multiple username targets.

# # skel Templates

When you use the `useradd` command and the `-m` option, a home directory is created for the user using the base directory and username. By default, the new home directory is a copy of the `/etc/skel` directory and its contents.

For example, `useradd -m snuffy` creates the home directory `/home/snuffy`. This home directory is copied by default from the `/etc/skel` directory, and the permissions are changed to suitable security for the user.

You can put just about anything in a new user's home directory by placing the files in the `/etc/skel` directory. It's even more elegant to create a set of `/etc/skel_xxx` directories to make creating certain groups of users easier.

For example, to make linking users to a shared directory easier, you might use the following steps: