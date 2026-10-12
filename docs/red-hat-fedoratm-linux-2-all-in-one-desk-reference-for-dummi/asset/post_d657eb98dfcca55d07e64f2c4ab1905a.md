
If you log in as `root`, you can also set up, examine, and remove `cron` jobs for any user. To set up `cron` jobs for a user, use this command:

```bash
crontab -u username filename
```

Here, `username` is the user for whom you install the `cron` jobs, and `filename` is the file that contains information about the jobs.

Use the following form of the `crontab` command to view the `cron` jobs for a user:

```bash
crontab -u username -l
```

To remove a user's `cron` jobs, use the following command:

```bash
crontab -u username -r
```

**Note:** The `cron` daemon also executes the `cron` jobs listed in the system-wide `cron-job` file `/etc/crontab`. Here's the default `/etc/crontab` file in Fedora Core (type `cat /etc/crontab` to view the file):

```bash
SHELL=/bin/bash
PATH=/sbin:/bin:/usr/sbin:/usr/bin
MAILTO=root
HOME=/

# run-parts
01 * * * * root run-parts /etc/cron.hourly
02 4 * * * root run-parts /etc/cron.daily
22 4 * * 0 root run-parts /etc/cron.weekly
42 4 1 * * root run-parts /etc/cron.monthly
```

The first four lines set up several environment variables for the jobs listed in this file. The `MAILTO` environment variable specifies the user who receives the mail message with the output from the `cron` jobs in this file.

The line that begins with a `#` is a comment line. The four lines following the `run-parts` comment execute the `run-parts` shell script (located in the `/usr/bin` directory) at various times with the name of a specific directory as argument. Each of the arguments to `run-parts` — `/etc/cron.hourly`, `/etc/cron.daily`, `/etc/cron.weekly`, and `/etc/cron.monthly` — are directories. Essentially, `run-parts` executes all scripts located in the directory that you provide as an argument.

Table 1-9 lists the directories where to locate these scripts and when they execute. You have to look at the scripts in these directories to know what executes at these periodic intervals.

| Directory Name | Contents |
| :--- | :--- |
| /etc/cron.hourly | Scripts execute every hour |
| /etc/cron.daily | Scripts execute each day at 4:02 a.m. |
| /etc/cron.weekly | Scripts execute weekly on Sunday at 4:22 a.m. |
| /etc/cron.monthly | Scripts execute at 4:42 a.m. on the first day of each month |

## Chapter 2: Managing Users

### In This Chapter

- Adding user accounts
- Understanding the password file
- Managing groups
- Exploring the user environment
- Changing user and group ownerships of files and directories

Fedora Core is a multiuser system, so it has many user accounts. Even if you are the only user on your system, many servers require a unique username and group name. Take, for example, the Apache Web server. It runs under the username `apache`. A whole host of system users are not for people, but just for running specific programs.

Also, users can belong to one or more groups. Typically, each username has a corresponding private group name. By default, each user belongs to that corresponding private group. However, you can define other groups for the purpose of providing access to specific files and directories based on group membership.

User and group ownerships of files are a way to make sure that only the right people (or the right process) can access the right files and directories. Managing the user and group accounts is a typical system administration job. It’s not that hard to do this part of the job, given the tools that come with Fedora Core. I show you how:

### Adding User Accounts

You get the chance to add user accounts when you boot your system for the first time after installing Fedora Core. The `root` account is the only one that you must set up during installation. If you didn’t add other user accounts during the initial boot, you can do so later on, using the User Manager or the `useradd` command to add new users on your system.

![](img/9f89727199836b0f871f1745838aa8b2_451_0.png)

Creating other user accounts besides `root` is a good idea. Even if you’re the only user of the system, logging in as a less-privileged user is good practice because that way you can’t damage any important system files inadvertently. If necessary, you can type the `su -` command to log in as `root` and then perform any system administration tasks.

### Using the User Manager to add user accounts

You can use the User Manager to add user accounts. To start the User Manager, log in as root at the graphical login screen and choose Main Menu→System Settings→Users and Groups from the GNOME panel. If you’re not logged in as root, the User Manager prompts you for the root password. If prompted, enter the password and click OK. Then the User Manager window appears.

The window has two tabs: Users and Groups (as shown in Figure 2-1). The Users tab displays the current list of users from the /etc/passwd file. The Groups tab lists the names of groups from the /etc/group. Initially, the User Manager filters out any system users and groups. However, you can turn off the filter by choosing Preferences→Filter System Users and Groups, so that the check mark next to that menu item disappears. Figure 2-1 shows the User Manager window with a listing of all user accounts, including the system ones.

![](img/9f89727199836b0f871f1745838aa8b2_452_0.png)

**Figure 2-1:** You can manage user accounts and groups from the User Manager window.

You can add new users and groups or edit existing users and groups from the User Manager window.

To edit the information for an existing user, follow these steps:

1. **Click the username in the list on the Users tab and then click the Properties button on the toolbar.**
   That user’s information appears in a User Properties dialog box (see Figure 2-2).
2. **Edit the information and click OK to make the changes.**

**Figure 2-2:** Edit an existing user's information in this dialog box.

![](img/9f89727199836b0f871f1745838aa8b2_453_0.png)

To add a new user, follow these steps:

1. Click the **Add User** button on the toolbar (refer to Figure 2-1).
   This action opens the Create New User dialog box (shown in Figure 2-3).

**Figure 2-3:** Create a new user account by filling in the information in this dialog box.

![](img/9f89727199836b0f871f1745838aa8b2_453_1.png)

2. Fill in the requested information.
   In particular, you must enter the username and the password. After filling in all the fields, click the **OK** button. The new user now appears in the list on the **Users** tab in the User Manager window.

![](img/9f89727199836b0f871f1745838aa8b2_453_2.png)

**Remember**

Notice the **Create a Private Group for the User** check box. It's checked by default, and that means each new user is in a separate private user group. Sometimes you want a user to be in a specific group, however, so that the user can access the files owned by that group. Adding a user to another group is easy. For example, suppose I want to add the username `naba` to the group called `wheel`. I simply type the following command in a terminal window:

```bash
usermod -G wheel naba
```

To remove a user account, click the username in the list on the Users tab that displays all user accounts (refer to Figure 2-1). Then click the **Delete** button on the toolbar.

### Using commands to manage user accounts

If you’re working from a text console, you can create a new user account by using the `useradd` command. Follow these steps to add an account for a new user:

1. **Log in as root.**
   If you’re not already logged in as `root`, type `su -` to become `root`.
2. **Type the following `useradd` command with the `-c` option to create the account:**
   `/usr/sbin/useradd -c “Ashley Barkakati” ashley`
3. **Set the password by using the `passwd` command, as follows:**
   `passwd ashley`
   
   You’re prompted for the password twice. If you type a password that someone can easily guess, the `passwd` program rejects it.

The `useradd` command consults the following configuration files to obtain default information about various parameters for the new user account:

- `/etc/default/useradd`: Specifies the default shell (`/bin/bash`) and the default home directory location (`/home`).
- `/etc/login.defs`: Provides system-wide defaults for automatic group and user IDs, as well as password-expiration parameters.

Examine these files with the `cat` or `more` commands to see what they contain.

You can delete a user account by using the `userdel` command. Simply type `/usr/sbin/userdel username` at the command prompt to delete a user’s account. To wipe out that user’s home directory as well, type `/usr/sbin/userdel -r username`.
