
**Using groupdel** If, for some reason, you need to delete an existing group from the system, you can do so using the `groupdel` command at the shell prompt. For example, to delete the dbus users group, you would enter `groupdel dbus.users`.

Let's practice managing groups in the following exercise.

### Exercise 9-2: Managing Groups from the Command Line

![](img/fb5404b3ce1e1e1d707f5abc39814a4a_393_0.png)

VIDEO For more information watch Exercise 9-2.

In this exercise, you will practice creating and modifying groups from the shell prompt of your Linux system.

Suppose your company is putting together a new research and development team that will be using your Linux system. You need to create a new group for users who will be members of this team. Complete the following:

- 1. Verify that you are logged in to your system.
- 2. If necessary, switch to your root user account with the `su –` command.
- 3. Create a new group named research by doing the following:
    - a. At the shell prompt, enter `groupadd research`.
    - b. Add your user account and the dtracy user account (created in the previous exercise) to the research group by entering `groupmod –A "dtracy,your_username" research` at the shell prompt.
    - c. Verify that the users were added to the group by entering `tail /etc/group` at the shell prompt. You should see the following:

```
research::1000:dtracy,tracy
```

### Chapter Review

I started this chapter discussing the need for a basic level of file system security on a Linux system. I reviewed a scenario where multiple users on the same system were able to access each other's files and the problems that were encountered as a result. The way to prevent these problems is to first control who can access the system and then control what they can access once they are in.

The first part is accomplished by using Linux user accounts. With user accounts, users must supply a valid username and password (called credentials) before they are allowed to access the system. This is called "logging in" or "authentication." I pointed out that the Linux operating system will customize the system environment based on the username of the user who logged in. Users will have access to their own home directory and a customized desktop environment. I pointed out that, by default, user home directories are located in /home, except for the root user, whose home directory is located in /root. You can view specific information about a particular user using the `finger username` command at the shell prompt.

I also pointed out that each Linux user account has a unique ID number called the UID. No two users on the system have the same UID on the same system. Some distributions, such as openSUSE, start UIDs for standard users at 1000 by default. Other distributions, such as Fedora, start UIDs at 500. No matter what distribution you're using, the root user's UID is always set to 0. You can view a user's UID (as well as group membership) using the `id username` command.

I then discussed the various locations where user accounts can be saved on a Linux system. Using local authentication, user accounts are saved in `/etc/passwd` and `/etc/shadow`. Using LDAP authentication, user accounts are saved in an LDAP-compliant directory service. Using NIS authentication, user account files are distributed among several systems using the NIS service. Using Windows Domain authentication, user accounts are stored in a central database on a Windows (or Linux Samba) domain controller.

I pointed out that, for the LPIC-1/CompTIA Linux+ exam, you only need to be familiar with the local authentication method. In this configuration, the `/etc/passwd` file contains your user account information while the `/etc/shadow` file contains your users' encrypted passwords. The `/etc/passwd` file stores user accounts in the following format:

```
Username:Password:UID:GID:Full_Name:Home_Directory:Default_Shell
```

I also pointed out that the `/etc/passwd` file contains both standard and system user accounts. Standard user accounts are used for login. System user accounts can't be used for login. Instead, they are used by system services when they need to access the file system.

The `/etc/shadow` file stores user password information in the following format:

```
Username:Password:Last_Modified:Min_Days:Max_Days:Days_Warn:Disabled_Days:Expire
```

The `/etc/passwd` and `/etc/shadow` files must stay synchronized. To do this, you should avoid editing these files directly with a text editor. Instead, you should use the various user and password management tools on your system. To check your files, you can use the `pwck` command. If you suspect your files are out of sync, you can use the `pwconv` command to add accounts from `/etc/passwd` to `/etc/shadow`.

I then discussed the different utilities you can use from the shell prompt to manage user accounts on your Linux systems. To add a user, you use the `useradd` utility. If you don't supply any options when creating a user with `useradd`, the defaults contained in the `/etc/default/useradd` and `/etc/login.defs` files are used.

To set a user's password, you can use the `passwd` utility at the shell prompt. To view the status of a user's account, you can use the `-S` option with `passwd`. To modify an existing user account, you use the `usermod` utility. To remove a user account, you use the `userdel` utility. By default, `userdel` will not remove a user's home directory when deleting an account. If you want to remove the user's home directory, you can use the `-r` option with `userdel`.

I then shifted gears and discussed the role of Linux groups. Groups ease system administration by allowing you to group together users who need a common level of access to files and directories in the file system. Linux groups are stored in `/etc/group`. Group records in `/etc/group` are represented using the following syntax:

```
Group:Password:GID:Users
```

Some distributions store group passwords in `/etc/group`. Other distributions store them in a separate file (in encrypted format) in `/etc/gshadow`, much in the same manner as user accounts are stored in `/etc/passwd` and `/etc/shadow`. You create groups in your Linux system using the `groupadd` command. If you don't specify any options with the `groupadd` command, the group is created using default parameters found in `/etc/login.defs`.

To add users to a group, you must use the `-A` option with the `groupmod` command at the shell prompt. You can also remove groups using the `groupdel` command.

### Accelerated Review

- You need to control who can access a Linux system and what they can do with files and directories in the file system after they are in.
- To authenticate to a system, a user must supply a username and password (called credentials).
- Linux restores user-specific information when a user logs in, such as a home directory and desktop environment.
- User home directories are created in /home by default.
- The root user's home directory is /root.
- You can use the `finger` command to view information about a user account.
- Every Linux user account has a unique user ID (UID) number assigned to it.
- The root user's UID is 0.
- The starting UID for standard users is 1000 on some distributions and 500 on others.
- You can use the `id` command to view a user's UID.
- You can use many different authentication methods with a Linux system.
- For your LPIC-1/CompTIA Linux+ exam, you need to know how to use local authentication.
- Using local authentication, user accounts are stored in `/etc/passwd` and `/etc/shadow`.
- The `/etc/passwd` file stores user account information.
- The `/etc/shadow` file stores encrypted user passwords.
- You can use the `pwck` utility to verify that `/etc/passwd` and `/etc/shadow` are synchronized.
- You can use the `pwconv` utility to copy missing users from `/etc/passwd` to `/etc/shadow`.
- You can use the `useradd` utility to add users to a Linux system.
- When used without any options, `useradd` uses the system defaults contained in `/etc/default/useradd` and `/etc/login.defs` to create user accounts.
