
Linux, such actions require root access, which most users don’t possess. An ordinary user can generally wipe out his or her own files, but not those of another user of the system and not those belonging to the system as a whole.

This final point is the most relevant to people using Linux as a desktop OS, and is the primary reason that posts to Usenet newsgroups from root accounts are often greeted with scorn, or at least admonitions to create and use an ordinary user account. My own system has an ordinary user account that I use for tasks such as Web browsing, reading email, writing, and so on. Suppose that I accidentally type a command such as

```
rm -r / home/rodsmith/dumbstuff
```

The intent was to delete a specific directory called dumbstuff but, because of a stray space, this command actually tells the system to wipe every file from all mounted filesystems. Linux will not let me do this if I’m logged on as an ordinary user. I’ll wipe out all my own files if I don’t catch the error in time, but I won’t damage the system as a whole. If I do everything as root, though, I can wipe out the system. Linux can be cryptic to new users, and it doesn’t always warn you that you’re doing something dangerous, so you should definitely create and use an ordinary user account, even if you’re using Linux as a desktop OS.

## Note

> Although I encourage you to use a user account whenever possible, most of the actions described in this book are system configuration actions, and therefore require that you be root to perform them. You can either log in directly as root or you can use the su command to gain root access. At a command prompt or xterm window, type su, and then press the Enter key. Linux prompts you for a password. Enter the root password, and anything you type in that xterm or command prompt takes on root authority. If you’re running in X, programs that are already running aren’t affected by this.

## Using linuxconf

Creating a user account is quite easy using linuxconf. Choose Config, Users accounts, Normal, User accounts to get the account list window (Figure 5.11). You can click an existing account to alter it or click Add to add a new one. Either way, linuxconf displays the User account creation tab shown in Figure 5.12 (it’s called User information if you modify an existing account, though).

### FIGURE 5.11

The User accounts tab shows all the usual user accounts, along with key information about them, such as their primary groups and user IDs.

### FIGURE 5.12

You can create an account by filling in a few pieces of information and clicking Accept.

The most important information for creating a new account or modifying an existing one is in the Base info subtab. You can enter the user's login name, full name, groups, home directory, shell, and user ID. For most of these fields, if you don't enter any information, linuxconf assigns an appropriate default value. For instance, the default group is a new group with the same name as the login name; and linuxconf assigns the first available user ID.

The additional subtabs on the User account creation tab provide additional options for fine-tuning the features of a user's account:

- Params tab—You can set parameters relating to password expiration here. By default, values of -1 or 99999 appear, indicating that the password won't expire. If you want to force users to change their passwords (which is a good policy in many environments), you can alter these values.
- Mail aliases—You can specify that mail coming into an account should be directed elsewhere, and you can set the name that appears on outgoing mail from an account to be something other than this account.
- Privileges—You can specify that the user be able or unable to perform certain administration-like actions, such as shutting down the computer or viewing system log files.

When you set up a Linux system as a server, and particularly as a file server, you need to consider how you'll implement security. These considerations interact with the options you set for user accounts, as described in "Account Creation Tips," later in this chapter.

When you click Accept to create the account, linuxconf prompts you to enter a password. You have to type it twice to be sure you typed it correctly.

## Creating an Account with Text-Mode Tools

If you don't want to or can't use linuxconf, you can use fairly standard textual tools for creating accounts. The principal of these is useradd, generally located in /usr/sbin. To create an account with useradd, you must specify all the parameters on the command line, as in the following:

```
useradd -u 521 -g 100 -d /home/amy -s /bin/bash -p password amy
```

The options you're most likely to use with useradd are

- -u—Indicates the user ID to be assigned.
- -g—Indicates the group ID to be assigned.
- -d—Indicates the home directory.
- -s—Indicates the default shell.
- -p—Indicates the starting password.
- -D—Modifies an existing account rather than creates a new one (this option takes no additional parameters).

The username comes last on the line, without an identifying dashed option.
