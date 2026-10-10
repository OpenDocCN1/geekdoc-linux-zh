
## sudo

Purpose: Run a single command as a different user.

Usage syntax: `sudo [OPTIONS] [COMMAND]`

```bash
$ whoami
nick
$ sudo whoami
[sudo] password for nick: ******
root
$ whoami
nick
```
Using sudo to run a command as the root user

The `sudo` command allows you to run a single command as another user. It is most commonly used to execute commands that require root privileges. In this example `whoami` is executed as root via the `sudo` command.

Using the `sudo` command is the recommended way to run commands that require elevated privileges as it limits the amount of time spent with root privileges. This greatly helps prevent disasters such as accidental deletion of important system files.

> **Note**: User (or group) accounts must be listed in the `/etc/sudoers` file in order to execute commands as root with `sudo`.

Common usage examples:
- `sudo [COMMAND]`: Run the specified command as root
- `sudo -u [USER] [COMMAND]`: Run a command as the specified user
- `sudo !!`: Run the last command as root

## id

**Purpose:** Display information about a user's identity.

**Usage syntax:** `id [OPTIONS] [USER]`

```bash
# id
uid=0 (root) gid=0 (root) groups=0 (root)
```
Displaying user and group information for the current user

The `id` command displays user and group information for the specified user. Executing `id` with no options displays the current user's information as displayed in the above example. The next example demonstrates using the `id` command to display information about a specific user.

```bash
# id nick
uid=1000 (nick) gid=1000 (nick) groups=4 (adm), 20 (dialout), 24 (cdrom), 46 (plugdev), 106 (lpadmin), 121 (admin), 122 (sambashare), 1000 (nick)
```
Displaying user and group information for a specific user

> **Note**
> 
> **Unix, Linux, and BSD** systems assign a numerical UID (**User ID**) and GID (**Group ID**) for each user and group on the system. A user friendly name is also assigned to each UID and GID which is displayed in parenthesis next to each ID number. This information is stored in `/etc/passwd` for users and `/etc/group` for groups.

Common usage examples:

| Command | Description |
| :--- | :--- |
| `id` | Display the current user's ID information |
| `id [USER]` | Display user and group information for the specified user |

## groups

**Purpose:** Display which groups a user belongs to.

**Usage syntax:** `groups [OPTIONS] [USER]`

```bash
# groups
root
```
Displaying group information for the current user

The `groups` command displays a user’s group membership. Executing `groups` with no options displays the current user’s groups, as shown in the above example. A user name can be used with the `groups` command to display the specified user’s group membership as shown in the next example.

```bash
# groups nick
nick adm dialout cdrom plugdev lpadmin admin sambashare
```
Displaying group information for the specified user

**Common usage examples:**

| Command | Description |
| :--- | :--- |
| `groups` | Display the current user’s group membership |
| `groups [USER]` | Display group membership for the specified user |

## who / whoami

**Purpose:** Display who is logged into the system.

**Usage syntax:** `who [OPTIONS]`

```bash
$ who
root  tty2  2010-05-17 11:32
nick  tty1  2010-05-17 11:31
nick  pts/0 2010-05-17 08:40 (10.10.1.251)
dave  pts/1 2010-05-17 12:32 (10.10.1.188)
mike  pts/2 2010-05-17 14:28 (10.10.1.167)
lisa  pts/3 2010-05-17 14:50 (10.10.1.204)
nick  pts/4 2010-05-17 15:33 (10.10.1.251)
```
Output of the who command

The `who` command displays information about users currently logged in to the system. The default output of the `who` command displays the username, terminal ID, and date/time the user logged in as shown in the above example.

> **Note**: Users logged in via telnet or SSH sessions will also display the IP address of the remote client in parentheses.

The `whoami` command displays the username of the current user. This is helpful to verify which user's environment and security privileges are available when switching between different accounts.

**Usage syntax:** `whoami`

```bash
$ whoami
nick
```
Using whoami to display the name of the current user

Common usage examples:
- `who`: Display who is currently logged into the system
- `who -b`: Display the last system boot time
- `who -r`: Display the current run level
- `whoami`: Display the name of the current user

## w

Purpose: Display detailed information about users logged in to the system.

**Usage syntax:** `w [OPTIONS] [USER]`

```bash
$ w  
15:39:12 up 4 days, 6:09, 5 users, load average: 0.06, 0.05, 0.01
```

| USER | TTY | FROM | LOGIN | IDLE | JCPU | PCPU | WHAT |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| nick | pts/0 | 10.10.1.251 | 08:40 | 1:10 | 0.18s | 0.15s | -bash |
| dave | pts/1 | 10.10.1.188 | 12:32 | 0.00s | 0.14s | 0.14s | vim |
| mike | pts/2 | 10.10.1.167 | 14:28 | 0.00s | 0.12s | 0.12s | tail |
| lisa | pts/3 | 10.10.1.204 | 14:50 | 9.00s | 0.14s | 0.14s | -bash |
| nick | pts/4 | 10.10.1.251 | 15:33 | 0.00s | 0.15s | 0.01s | w |

Output of the `w` command

The `w` command shows detailed information about users logged into the system. It is similar to the previously discussed `who` command except it provides additional information such as the user's last login time, how long they have been idle, and what program they are currently running.

The `w` command also displays a system summary line that shows the host's uptime, number of connected users, and samples of system load averages for the past 1, 5, and 15 minutes.

> The information displayed on the first line is the same output generated by the `uptime` command. See page 215 for more information about system uptime and load averages.

**Common usage examples:**

- `w`: Display detailed information about users currently logged in to the system

## last / lastb

Purpose: Display the last successful/failed user logins.

**Usage syntax:** `last [OPTIONS] [USER]`

```bash
$ last
nick    pts/1      192.168.1.50   Sat May 22 13:42   still logged in
nick    pts/0      192.168.1.50   Sat May 22 13:42   still logged in
nick    tty7        :0            Sat May 22 13:40   still logged in
reboot  system boot  2.6.32-21-ge  Sat May 22 13:40 -  14:02  (00:21)
nick    pts/0      :0.0          Thu May 20 21:33 -  21:56  (00:03)
nick    pts/0      :0.0          Thu May 20 21:30 -  21:33  (00:02)
root    pts/0      :0.0          Thu May 20 21:27 -  21:30  (00:03)
nick    tty7        :0          Thu May 20 21:25 - crash (1+16:14)
...
```
Output of the last command

The `last` command displays the login and logout times for each user on the system. It also shows information about system shutdowns and restarts as shown in the above example.

The `lastb` command displays failed login attempts as shown in the next example.

**Usage syntax:** `lastb [OPTIONS] [USER]`

```bash
$ lastb
nick    tty1       Sat May 22 13:59 -  13:59  (00:00)
nick    tty1       Thu May 20 21:27 -  21:27  (00:00)
root    tty1       Thu May 20 15:27 -  15:27  (00:00)

btmp begins Sat May 20 13:59:28 2010
```
Output of the lastb command

> **Note**: User login/logout activity is stored in the `/var/log/wtmp` file. Failed login attempts are logged in `/var/log/btmp`.

Common usage examples:
- `last`: Display the last user login information
- `last -[NUMBER]`: Display the specified number of logins
- `last [USER]`: Display the last logins for the specified user
- `lastb`: Display failed login attempts
- `lastb -[NUMBER]`: Display the specified number of failed login attempts
- `lastb [USER]`: Display failed login attempts for the specified user

## lastlog

Purpose: Display the most recent user login information.

Usage syntax: `lastlog [OPTIONS]`

```bash
$ lastlog | more
Username Port From Latest
root tty2 Sat May 30 11:32:33 -0500 2009
dave tty3 Sat May 30 10:22:51 -0500 2009
nick pts/0 10.10.1.251 Sat May 30 11:31:51 -0500 2009
steve **Never logged in**
bin **Never logged in**
sync **Never logged in**
lp **Never logged in**
...
```

![](img/fa2f95b64a707c963dfa0445bd9281a7_96_0.png)

The `lastlog` command displays the most recent user login time and dates for every user on the system. Executing `lastlog` with no options displays the last login information for all users, as shown in the above example. This output is similar to the `last` command except `lastlog` only displays the most current login activity where `last` displays all available login events.

The `-u` option can be used to display the last login for a specific user as demonstrated in the next example.

```bash
$ lastlog -u nick
Username Port From Latest
nick pts/0 10.10.1.251 Sat May 30 11:31:51 -0500 2009
```

![](img/fa2f95b64a707c963dfa0445bd9281a7_96_1.png)

Common usage examples:
- `lastlog`: Display the last login information for all users
- `lastlog -u [USER]`: Display the last login information for the specified user
