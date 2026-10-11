
user cannot make system changes directly. In the initial years of Linux, the solution to this challenge was to allow the regular user to switch to the root user through the `su` command until the required task was completed. This was seen as a disadvantage since a regular user could become a root user with all the privileges. This meant that they could make any changes to the system and even delete important directories. Also, switching to the root user via the `su` command meant that a regular user would then know the root user account's password. This was definitely not a practical solution.

This was when Linux introduced the concept of `sudo`. The `sudo` command simulates a regular user to be the root user and run specific root commands. The settings for `sudo` are defined in the file stored at `/etc/sudoers`. While the `su` command needed you to know the root user's password, the `sudo` command requires you to know only your password. This means the root user can assign certain privileges to regular users via `sudo` to perform system-related tasks without giving away the root password.

Let us look at the example below where a student user is running the `usermod` command through `sudo` access. The student user can use this access to modify another user account and lock that account.

```bash
[student@desktop ~]$ sudo usermod -L username
[sudo] password for student: studentpassword
```

Running commands through `sudo` has a huge benefit as well. All the commands that are run on a Linux system using `sudo` are logged in a file at `/var/log/secure`.

## User Account Management

This section will teach you how you can create, modify, and delete user accounts that exist on a Linux operating system. You can manage local user accounts in Linux via numerous tools on the Linux command line. Let us go through them in brief.

### useradd username

This command is used to add a new user to the system. The username that is passed along with the command is used to create the new user. The user gets created with the default parameters with the respective values in the file at `/etc/passwd` when you do not use any other options with the command. Note that this command will not set a password for the new user and, the user will not be able to login into the Linux system until a password is set.

You can type the `useradd --help` command to get the manual for the `useradd` command that will give you a list of options that you can pass with this command. If you manually pass options for the `useradd` command, they will override the user's default properties in the `/etc/passwd` file.

Some parameters for a user, such as the UID and password aging policy, are picked up from the file at `/etc/login.defs`. This file is used only when a new user is created. Modifying this user does not affect the properties of the existing users on the system.

### usermod username

This is a command that can be used to change existing users' properties in the Linux system. You can type the command `usermod --help` to get a list of all the options that can be used with this command. Let us see these options.

| Option | Description |
| :--- | :--- |
| `-c, --comment COMMENT` | This option is used to add a value such as full name to the GECOS field |
| `-g, --gid GROUP` | The primary group of the user can be specified using this option |
| `-G, --groups GROUPS` | Associate one or more supplementary groups with user |
| `-a, --append` | The option is used with the `-G` option to add the user to all specified supplementary groups without removing the user from other groups |
| `-d, --home HOME_DIR` | The option allows you to modify a new home directory for the user |
| `-m, --move-home` | You can move the location of the user's home directory to a new location by using the `-d` option |
| `-s, --shell SHELL` | The login shell of the user is changed using this option |
| `-L, --lock` | Lock a user account using this option |
| `-U, --unlock` | Unlock a user account using this option |

### userdel username

As the command suggests, this will delete the user account and its record from the `/etc/passwd` file; but this command does not delete the user’s home directory. You can use the `userdel -r username` command to delete the user from the `/etc/passwd` file and delete their home directory too.

### id

This command, as we discussed earlier, displays the details of the user that is currently logged in. Using another username along with the `id` command will show the basic details of the other user as well.

### passwd username

This command can be used to set the initial password for a user that you create. It can also be used to modify the password for an existing user.

The root user can modify any user’s password and set it to any value. If the password strength criterion is not met, a warning will be shown, but the root user can simply retype the same password to set it for the user anyway.

If a regular user is trying to set a password, it will have to meet the criteria of having at least eight characters, it should not match the username, and it should not be a word that can be found in a dictionary.

### UID Ranges

These are ranges that are reserved for specific purposes in a Linux operating system.

- UID 0 is always assigned to the root user.
- UID 1-200 is statically assigned by the system to system processes.
- UID 201-999 are assigned to the system process that does not own any file in the system. They are dynamically assigned whenever installed software requests for a process.
- UID 1000+ are assigned to regular users of the system.

## Group Management

Like in the case of users, you can also create, modify, or delete groups on the system at a local level.

Remember that it is important for a group to exist before you can add users to that group. You can manage local groups through several tools in Linux. Let us go through these commands that are used for groups.

### groupadd groupname

This command is used to add a new group. The groupname passed with the command is created on the system, and a GID is assigned to it. The group is defined in the file stored at `/etc/login.defs`.

You can also specify a particular GID by using the following option `-g GID`.

```bash
[student@desktop ~]$ sudo groupadd -g 5000 team
```

You can also use the `-r` option along with this command to create a system-specific group, and the GID assigned to it will be from a range of system values for GID.

```bash
[student@desktop ~]$ sudo groupadd -r professors
```

### groupmod

This command can be used to modify the properties of a group that already exists in the system. You can use this command to perform tasks like changing the groupname’s mapping to a GID. You can use the `-n` option with this command to change the name of the group.

```bash
[student@desktop ~]$ sudo groupmod -n professors lecturers
```

You can also pass the `-g` option with this command if you want to change the GID for an existing group.

```bash
[student@desktop ~]$ sudo groupmod -g 6000 ateam
```

### groupdel

This command is used to delete a group from the Linux system.

```bash
[student@desktop ~]$ sudo groupdel ateam
```

Note that the `groupdel` command may not work on the primary group of the user. Just like in the case of `userdel`, you need to ensure that a user does not own any files after you delete a group.

### Usermod

This is a user command but can be used to modify the group of a user. This can be done through the command `usermod -g groupname`.

```bash
[student@desktop ~]$ sudo usermod -g student student
```

You can also use this command to add a user to a supplementary group through `usermod -aG groupname username`.

```bash
[student@desktop ~]$ sudo usermod -aG wheel student
```

The `-a` option ensures that the modifications are being appended to the user’s properties. If you do not use the `-a` option, the user will be added to the specified group and will be deleted from all other groups.

## Password Management for User

This section will take you through how the password for a user on the Linux system is managed. We will cover the shadow password file used to password aging policies for a user and can also be used to manually lock a user account. In the beginning, Linux systems stored the encrypted password for a user in the file at the `/etc/passwd`, which was accessible to everyone. It was a secure path for a long time until attackers started targeting this file with dictionary attacks. This was when Linux developers decided to move the password to a more secure location at the `/etc/shadow` file. This new file has
