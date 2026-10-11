To add a user, simply add a new line at the end of the file that contains the appropriate information for each field. Be sure to use an editor that saves the information in ASCII, such as vi. Do not enter anything in the password field because it needs to be encrypted. You will need to enter a unique UID for each new user you add to the file. Keep a record of assigned UIDs and assign new ones sequentially. To create a new account for me, you might add the following line to your `/etc/passwd` file:

```
`hadden::523:100:Theresa Hadden:/home/hadden:/bin/bash`
```

After entering the user information and saving the file, you will need to use the passwd command to assign a password to the new account.

Next, you will need to create the user's home directory and manually copy the appropriate configuration files. These configuration files are discussed later in this chapter.

If a new group is also needed for this user, you will need to edit the `/etc/group` file to define the group before the user can log in. Groups are discussed later in this chapter.

If you manually create a user's home directory, you will need to change both the owner and group assigned to that directory or the user will be unable to log in. Use the chown command to change both the user and associated group. See Chapter 9 for more information on using this command.

# Key Concept

New user accounts can be created by editing the `/etc/passwd` file and then using the `passwd` command to assign a password to the account. You also will need to create the user's home directory and assign the appropriate permissions to this directory before the user will be able to log in.

# Using the `useradd` Command

Another, more convenient way to add user accounts to your system is by using the useradd command. By default, useradd uses the next available UID and assigns the default shell as the login command for that account. To display the system's default values, type useradd -D without a username. Its output might look like the following:

```
```
GROUP=100
HOME=/home
INACTIVE=-1
EXPIRE=
SHELL=/bin/bash
SKELE=/etc/skel
```
```

![](bbox=[0.95, 0.7, 1.0, 0.98])