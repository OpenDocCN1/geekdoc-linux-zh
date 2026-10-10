
## Deleting a User Account

- Log in as the root user.
- Type: `userdel -r USER`.

> **Warning**
> The `-r` option removes the user's home directory and the files in it. If you want to keep the home directory, omit the `-r` option.

## Editing a User Account

Log in as the root user. Then type: `usermod OPTIONS USER`.

The options are the features to edit. The options are similar to those of the `useradd` command.

### The usermod Command (Edits User Accounts)

| Option | Action | Comment |
| :--- | :--- | :--- |
| `-G GROUPS` | Adds groups in addition to the initial one. | Enter multiple groups by name or GID. Separate the names with a comma and leave no blank spaces. |
| `-g GROUP` | Changes the default group. | Enter multiple groups by name or GID. Separate the names with a comma and leave no blank spaces. |
| `-d DIRECTORY` | Changes the home directory. | |
| `-l NEW_NAME` | Changes the user name. | The user must be logged out to use this option. |
| `-e DATE` | Sets an expiry date for the user account. | |
| `-f NUMBER` | Sets the number of days after the expiry date that the account is disabled. | Use with the `-e` option, which sets an expiry date. |
| `-u UID` | Sets the user ID. | The user should not be executing any command when this option is used. Must be a unique ID. Files in the user’s home directory are changed, but not files elsewhere. |
| `-s SHELL` | Sets the users’ shell. | If no shell is specified, then the default BASH is used. |

## Changing Individual Passwords

1. Type `passwd USER`. You are prompted for (current) UNIX password.
   You do not need to enter the user for the current account. For information about selecting a password,
2. Enter your current password. You are prompted for your New UNIX password.
3. Enter your new password. You are prompted to retype new UNIX password.
4. Enter your new password again. A message displays: All authentication tokens updated successfully.

The next time you log in to the account whose password you have changed, you must use the new password.

## Choosing a Password

A good password is one that is hard to crack. That is, it is:

- A mixture of letters, numbers, symbols, and of upper and lower case.
- At least six characters long.
- Not based on anything associated with you, such as a birthday, a spouse’s name, a pet, or a favorite sports team or movie.
- Not a common word found in a dictionary.
- Different from your passwords on other machines.
- Different to your user account.
- Not written down anywhere.

## Managing Groups

User groups can define:

- How users can access the system.
- What files, directories, and services users can work with.
- What hardware users can work with.

Some of these features are defined when the group is created. Others are created by using permissions or configuration settings.

Groups are listed in the `/etc/group` file. Each group has a unique ID (GID).

### Reading the /etc/group File

The `/etc/group` file lists all existing groups. By default, any user can view this file, but you must be logged in as the root user to edit it.

Each group is defined in a line in `/etc/group`. Columns are separated by a colon. Information is given in the following order:

`GROUP: ENCRYPTED_PASSWORD: GROUP_ID: USERS_IN_GROUP.`

Note:

- The group name generally reflects what access the group has to the system. For example, the lp group defines who can use the printer.
- The encrypted password is rarely used any more. Usually, an x is added as a placeholder.
- The group ID is usually a number from 1 to 50.
- The list of users in the group only needs to contain those who are not in the group by default.

You can edit `/etc/group` directly in a text editor. However, often, the command line tools are easier to use.

### Adding a Group

1. Log in as root user.
2. Type: `groupadd -g GID GROUP`.

You can create a group without a group ID by leaving out the option.

### Deleting a Group

1. Delete the group. Logged in as root user, type: `groupdel GROUP`.
2. Find files that belong to the group. Type: `find -l -group GROUP`. See “Searching for Files and Text,” page 167.
3. Change the group ownership on the files. See “Changing Groups,” page 225. To save effort, select multiple files.

### Editing a Group

1. Select the group. Logged in as root user, type: `groupmod -g GID`.
2. Find files that belong to the group. Type: `find -l -group GROUP`. See “Searching for Files and Text,” page 167.
3. Change the group ownership on the files. See “Changing Groups,” page 225. To save effort, select multiple files.

## Managing Printing

Linux includes a number of command line tools for administering printing. These commands are useful on networks, or for troubleshooting and managing printing on any system.

Each printer on a Linux system has its own spool or queue in the `/var/spool/lpd` directory. This spool uses the short name of the printer, which is created when the printer is first configured. When a file is printed, it becomes a job in the spool. Each job is stored in a spool until it is printed.

Printing tools generally start with `lp` (short for “line printer”). If you are familiar with other Linux commands, you can usually make a good guess at what the rest of the command should be. For example, `lprm` removes a print job from the spool.

You can use the following tools for managing printing:

- `lpq`: Checks the status of print jobs.
- `lprm`: Removes a print job from a spool.
- `lpstat`: Reads the status of a spool.

### Checking the Status of Print Jobs

Type: `lpq OPTIONS USER`.

The command's name comes from the fact that a spool is sometimes called a “queue.”

#### The lpq Command (Print Jobs)

| Option | Action | Comments |
| :--- | :--- | :--- |
| `-l` | Print information for each file in the printer queue | |
| `NUMBER` | To check the status of a job number | |
| `-P PRINTER` | To set the printer that a job should use. | Not needed if the default is used. |

### Removing Jobs From a Printer Spool

Type: `lprm OPTIONS JOB USER`.

The command's name comes from the fact that it removes (m) a job from a line printer (lp).

Only the root user can remove a job sent by another user. Regular users can remove their own print jobs.

Use `lptest` to find job numbers. See “Reading the Status of a Printer Spool,” page 305.

#### The lprm Command (Remove Print Jobs)

| Option | Action | Comments |
| :--- | :--- | :--- |
| `-P PRINTER` | Sets the printer to use | Not needed if the default is used. |
| `-USER` | Removes all jobs sent by the user specified. | |

### Reading the Status of a Printer Spool

Type: `lptest -t OPTIONS`.

### Printing From the Command Line

Type: `lpr OPTIONS FILES`.

#### The lpr Command (Print)

| Option | Action | Comments |
| :--- | :--- | :--- |
| `-P PRINTER` | Selects the printer to use. | Otherwise, the system default is used. |
| `-S` | Sends a symbolic link to the printer instead of the file. | This option saves time and disk space for large files, but may cause printing to be slower. |

## Managing Processes

A process is a running program to which the Linux kernel has assigned a share of your system's resources or computing power. Because Linux is a multi-tasking operating system, dozens of processes can be running at any one time.

Some of the reasons that you may want to check the processes that are running include:

- **To Troubleshoot:** Your system is not responding properly. The processes, the combination of processes, and the resources used by processes should all be examined as a routine part of troubleshooting.
- **To check system security:** If you suspect an intruder on the system, the processes used may provide a clue. You should also check what user or group ID a process is running under. In particular, check programs running under the root account, since they could do the most damage.
- **To close a frozen or strangely behaving program:** while Linux itself is stable, the desktop has developed rapidly, and some programs that run under the X Window System behave erratically. You may also need to close a program while testing it.

### Understanding Processes

Linux uses three basic types of processes:

- **Interactive:** An ordinary program started by a user. Many commands entered from the command line are interactive processes. So is each new window opened in the X Window system.
- **Batch:** Any process run without a command line terminal.
- **Daemon:** A process that runs continuously. Usually, they are started when the system starts, but they can also be started by the root user. Daemons generally run in the background.

You should also know:

- **A major characteristic of each process is its priority.** If system resources are short, the priority determines what share of the resources the process
