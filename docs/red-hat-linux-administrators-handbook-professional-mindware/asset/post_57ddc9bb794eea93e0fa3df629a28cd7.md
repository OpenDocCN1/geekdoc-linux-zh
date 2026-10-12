
## groupmod

For example, the following renames the existing novices group to experts:

```
groupmod -n experts novices
```

To change the GID, use the `-g new GID` option. For example, the following changes the current GID of the troublemakers group to 666:

```
groupmod -g 666 troublemakers
```

## groups

**Syntax:** `groups [username]`

The **groups** command displays the list of group(s) the named user currently belongs to. If no username is specified, the current user's groups are displayed.

## last

**Syntax:** `last [-number] [username] [reboot]`

The **last** command displays a list of users who have logged in since `/var/log/wtmp` was created. For example, the following command shows the number of times user julie has logged in since the last time `/var/log/wtmp` was created:

```
last julie
```

The following command shows only the last ten logins by julie:

```
last -10 julie
```

This command displays the number of times the system was rebooted since `/var/log/wtmp` file was created:

```
last reboot
```

## passwd

**Syntax:** `passwd username`

The **passwd** command allows you to change a user's password. Only a superuser can specify a username; everyone else **must** type `passwd` without any argument, which allows the user to change her own password. A superuser can change anyone's password using this program.

## su

**Syntax:** `su [ - ] [ username ]`

The `su` command can become another user. For example,

```
su john
```

allows you to be the user *john*.

The most common use of this command is to become root. For example, if you run this command without any username argument, it assumes that you want to be root and thus prompts you for the root password. If you enter the correct root password, `su` will run a shell using the root's UID (0) and GID (0). This effectively allows you to become the root user and perform administrative tasks. This command is very useful if you have only Telnet access to the server. You can Telnet into the server as a regular user and use it to become root to perform system administrative tasks. If you supply the `-` option, the new shell is marked as the login shell. After you become the root user, you can `su` to other users without entering any password.

## useradd

To create a user account from your command line, run the `useradd` command. For example, to create a user called `newuser`, run:

```
useradd newuser
```

This adds a new entry in `/etc/passwd` (and in `/etc/shadow` if you use shadow passwords) using system defaults. For example, when I run the preceding command on my Red Hat system, `/etc/passwd` shows a new line such as the following:

```
newuser::11:506:506::/home/newuser:/bin/bash
```

If you remember the `/etc/passwd` fields from the earlier discussion, you will see that the password field (the second field) is set to `!!`. This means that this password is not set and newuser cannot log in yet. So, you need to create a password for this user by running the `passwd` command as follows:

```
passwd newuser
```

You are asked to enter the password twice, and after your password is accepted, it is encrypted and added to the user's entry in the `/etc/passwd` file.

The UID and GID values will be automatically selected by `useradd`. Basically, it just increments the last UID in `/etc/passwd` by 1 and the last GID in `/etc/group` by 1 to create the UID and GID, respectively, for the new user. You can also manually set the UID and group using the command-line switches `-u` and `-g` respectively. The home directory is created in the default top-level home directory. Similarly, the login shell is selected from a system default. If you want to override a system default, specify a command-line option. To override the default home directory, use the `-d newdirectory` option (where `newdirectory` is the name of your directory). For example:

```
useradd newuser -d /www/newuser
```

The new user (`newuser`) will be created, and her home directory will be set to `/www/newuser`. Note that `useradd` will create only the final directory, not the entire path. For example, if you specify `-d /some/new/dir/myuser` as the option, `useradd` will create `myuser` only if `/some/new/dir` already exists.

When the new home directory is created, files contained in the `/etc/skel` directory are copied to the new home directory. These files are typically the dot configuration files for the default shell. For example, if the default shell is `/bin/bash`, you should have default versions of `.bashrc`, `.bash_profile`, and `.bash_login` in the `/etc/skel` directory so that the new user's home directory can be automatically set up with these files.

The `useradd` that comes with Red Hat Linux creates a private group for the user with the same name as the username. For example, if you run `useradd kabir`, a new user named `kabir` will be created in the `/etc/passwd` file, and a new group called `kabir` will be created in the `/etc/group` file. This method allows the new user to be totally isolated from the rest of the users and therefore ensures greater privacy for the user. Whenever the new user creates a new file, by virtue of this private group, the file is accessible only by the new user. The user has to change the file permissions explicitly in order to allow someone else to see the file.

However, if your user account clashes with this kind of private group idea, you can override it by using the `-g group` option (where `group` is the name of your group). For example,

```
useradd mjkabir -g users
```

makes `useradd` create the new user (mjkabir) with the default group set to the users.

If you want to make the new user a member of additional groups on your system, use the `-G comma-separated list of groups` option. For example,

```
useradd mjkabir -G wheel,admins
```

adds the new user (mjkabir) to the `wheel` and `admins` groups in the `/etc/group` file.

## userdel

To delete an existing user, use the `userdel` command. For example, the following deletes the user called `snake`:

```
userdel snake
```

If you want to remove the user's home directory and all of its contents, use the `-r` option. Note that `userdel` will not delete the user if the user is currently logged in. Ask the user to log out by sending her a `write` message (`write username`), and if asking isn't an option, use the `killall` command to terminate all processes associated with the user, then run the `userdel` command.

To temporarily disable a user account, do one of the following:

- Use the `usermod -s new shell username` command to change the shell to `/bin/false` (make sure the new shell is listed in the `/etc/shells` file). This disallows the user from logging in to the system.
- If you are using shadow passwords, use the `usermod -e MM/DD/YY username` command to cause the user account to expire.

To disable all user account access temporarily, create a file called `/etc/nologin` with a message explaining why you are not allowing access. The login program will not allow any nonroot account to log in as long as this file is in place.

## usermod

The `usermod` command is used to modify a user account. To change the home directory of an existing user, run the `usermod` command as follows:

```
usermod -d new_home_directory username
```

where `new_home_directory` and `username` are the correct values.

For example, if a user called `keller` has `/home/keller` as her home directory, and you want to move it to `/home2/keller`, run the `usermod` command as follows:

```
usermod -d /home2/keller keller
```

This sets the new directory as her home directory. However, if you want to move the contents of her home directory to the new location, use the `-m` option as follows:

```
usermod -d -m /home2/keller keller
```

To change the UID of a user, use the `usermod` command as follows:

```
usermod -u UID username
```

where `UID` and `username` are the correct values.

For example, the following changes the UID for user `mrfrog` to 500:

```
usermod -u 500 mrfrog
```

All the files and directories that are owned by the user within her home directory will automatically reflect the UID change. However, if the user owns files outside her own home directory, you will have to manually change the ownership using the `chown` command.
