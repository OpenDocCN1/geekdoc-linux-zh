
Example 9-1 displays the partial output of the `configure` command. Even though we show this example with PAM enabled, we will look at `sudo` with and without the use of PAM. Notice that we have specified a more restrictive `umask` (0027), so that when commands that create files are executed via `sudo`, they will have no world permissions. The `--with-ignore-dot` option is incorporated to exclude "." from root's `PATH` when `sudo` is invoked. And, we include insults for fun!

### Example 9-1 Configuring `sudo`

```bash
# ./configure --with-pam --with-insults --with-umask=0027 --with-ignore-dot
creating cache ./config.cache
Configuring CU Sudo version 1.5.9
Checking whether to use PAM authentication... yes
<lots of output snipped>
...  
 creating Makefile
creating config.h
creating pathnames.c
You will need to customize sample.pam and install it as /etc/pam.d/sudo
```

Now that `configure` has built the `Makefile`, among other files, we are ready to compile. Example 9-2 shows the execution of `make`.

### Example 9-2 Compiling and Linking `sudo` with `make`

```bash
# make
gcc -c -I. -I.  -g -O2 -D_PATH_SUDO_SUDOERS="/etc/sudoers" -D_PATH_SUDO_STMP="/etc/stmp" -DSUDOERS_UID=0 -DSUDOERS_GID=0 -DSUDOERS_MODE=0440  sudo.tab.c
gcc -c -I. -I.  -g -O2 -D_PATH_SUDO_SUDOERS="/etc/sudoers" -D_PATH_SUDO_STMP="/etc/stmp" -DSUDOERS_UID=0 -DSUDOERS_GID=0 -DSUDOERS_MODE=0440  lex.yy.c
...
<lots of output snipped>.
...
gcc -c -I. -I.  -g -O2 -D_PATH_SUDO_SUDOERS="/etc/sudoers" -D_PATH_SUDO_STMP="/etc/stmp" -DSUDOERS_UID=0 -DSUDOERS_GID=0 -DSUDOERS_MODE=0440  visudo.c
gcc -o visudo sudo.tab.o lex.yy.o visudo.o
```

Once compiled and linked, we can install. Example 9-3 shows the output of a successful `sudo` install.

### Example 9-3 Installing `sudo`

```bash
# make install
./mkinstalldirs /usr/local/bin /usr/local/sbin /etc /usr/local/man/man8 /usr/local/man/man5
./install-sh -c -o 0 -g 0 -m 0411 -s sudo /usr/local/bin/sudo
./install-sh -c -o 0 -g 0 -m 0411 -s visudo /usr/local/sbin/visudo
./install-sh -c -o 0 -g 0 -m 0444 ./sudo.man /usr/local/man/man8/sudo.8
./install-sh -c -o 0 -g 0 -m 0444 ./visudo.man /usr/local/man/man8/visudo.8
./install-sh -c -o 0 -g 0 -m 0444 ./sudoers.man /usr/local/man/man5/sudoers.5
```

Now we're ready to use it!

## USING sudo

Before we can take a look at some sudo examples, we need to explore how sudo works and how we configure sudo with the /etc/sudoers file.

### The Functionality of sudo

The sudo command allows an authenticated user to execute an authorized command as root. Both the effective and the real UID and GID are set to 0 (yes, you really are root). It determines which users are authorized and which commands they are authorized to use through its configuration file /etc/sudoers. When a user executes sudo, that user will be required to enter his or her password (by default, with PAM or other compile time options, this can change). Once the user is successfully authenticated, then sudo will execute the requested authorized command and exit. The user may request other commands using sudo, including a root shell, and not be required to reauthenticate himself or herself for 5 minutes (default; this is a compile time option; see the INSTALL.configue file in the sudo source distribution).

When executed, the sudo utility attempts to safely run commands by eliminating certain potentially dangerous environment variables, including IRS, ENV, BASH_ENV, and all LD.* and RLD.* variables (used for dynamic loading).

If a user executes sudo and that user does not appear in the /etc/sudoers file, then mail is sent from that user to root (by default, see Table 9.1 on page 175), informing the administrator of an access violation. This event is also logged through syslog.

Each time sudo is executed, the entire command, including flags and arguments, is logged via syslogd. Included in the log entry are date and timestamp, username, terminal name, current working directory, and an error message, if any.

### The /etc/sudoers File

The /etc/sudoers file is very feature rich. For that reason, it is often overwhelming when all the available bells and whistles are described up front. So we will start with a few simple examples and work our way toward more complex ones.

Let's suppose that you need to set up /etc/sudoers for a single system, called fghhmn. On this system, the users bill and mary share the administrative responsibilities. There are two bin users, jane and paul, who are responsible for maintaining the database and making sure that the printer functions properly. In Example 9.4, we see a simple /etc/sudoers file that allows for bill and mary to execute any command as any user. On the other hand, jane and paul have privileges limited to the execution of the database commands and the printer maintenance commands. We'll break down this file

```bash
# Simple sudoers file
# Modify with visudo only!
#
# Aliases Section
# User aliases
User_Alias    ADMINS=bill,mary
User_Alias    INTERNS=jane,paul
#
# Runas alias
Runas_Alias   MAINT=root,dmgr
#
# Command aliases
Cmd_Alias     LP=/usr/sbin/lpc,/usr/bin/lpr
Cmd_Alias     SHUT=/sbin/shutdown -r *
#
# Privilege Specifications
ADMINS        foghorn=(ALL) ALL
INTERNS       foghorn=(MAINT) LP,SHUT,/usr/local/db/bin/
```

into the components specified, namely *User Aliases*, *Runas Aliases*, *Command Aliases*, and *Privilege Specifications*.

*User Aliases.* This section simply sets up alias names for the users who will be granted privileges. User aliases require the `User_Alias` keyword. In Example 9-4, *bill* and *mary* belong to the `ADMINS` alias while *jane* and *paul* belong to the `INTERNS` alias. Alias names may be anything except `ALL` which is a reserved keyword.

*Runas Aliases.* In Example 9-4, there is one example of a runas alias that requires the `Runas_Alias` keyword. It specifies the list of users—who and `dmgr` in this case—who may be specified with the `sudo -u` invocation (described in *Options to the sudo Command* on page 184).

*Command Aliases.* These aliases are used to specify lists of commands and require the `Cmd_Alias` keyword. In this case, the `LP` alias expands to the two commands, `/usr/sbin/lpc` and `/usr/bin/lpr`. The `SHUT` alias expands the very specific command, `/sbin/shutdown -r *` (reboot).

*Privilege Specifications.* This section of the file indicates who gets what privileges on which hosts. In Example 9-4, the `ADMINS` may run any command as any user on the host `foghorn`. The `INTERNS` may run only the commands `/usr/sbin/lpc, /usr/bin/lpr` (expansion of `LP`), `/sbin/shutdown -r *` (expansion of `SHUT`), and any command in the directory `/usr/local/db/bin/` (these being the database commands). Furthermore, the `INTERNS` may execute these commands on the host `foghorn` only as either the user `root` or `dmgr` (expansion of `MAINT`). Note that the * in the specification of `/sbin/shutdown -r;` * expands to match 0 or more characters (same metacharacter definition in the shell). It is required because the `shutdown` command requires a time argument such as `now` or `+60` (60 minutes from now). See the `shutdown` man page for details.

### Examples for the Users in INTERNS

Let's first see what happens when the user paul tries to restart the printer daemons without using sudo. Example 9-5 displays the output of this attempt. Paul does not have the necessary permissions to kill and restart the lpq daemon, because it is owned by root. Since Paul has been granted permissions to do this in the /etc/sudoers file, he can accomplish his task by using sudo. Example 9-6 shows the user paul restarting the printer daemons using sudo. When sudo is executed for the first time, it displays the lecture message and then prompts paul for his password. At this point, paul may execute additional sudo commands without the lecture and password prompt for up to 5 minutes. Paul can extend this time limitation by using sudo -v. Even this command will require a password if the 5-minute limitation has lapsed.

### Example 9-5 Insufficient Permissions to Restart lpq

```
[paul@fohgnrn]$ /usr/sbin/lpc restart all
lp:
/usr/sbin/lpc: connect: Permission denied
[paul@fohgnrn]$ 
```

### Example 9-6 Successful lpq Restart Using sudo

```
[paul@fohgnrn]$ sudo /usr/sbin/lpc restart all
We trust you have received the usual lecture from the local System
Administrator. It usually boils down to these two things:

#1) Respect the privacy of others.
#2) Think before you type.
Password: paul's password
lpq:
daemon aborted
lpq:
daemon started
[paul@fohgnrn]$ 
```

Suppose that Paul needs to reboot the system. Based on the /etc/sudoers file, he is allowed to execute /sbin/shutdown -r. Let's see what happens in Example 9-7 if he executes the shutdown command without the -r flag. At this point, Paul is uncertain about why he can't reboot the system. After all, Mary told him that he had the permission to do that. So Paul decides to see what privileges he actually has by executing sudo -1, as shown in Example 9-8. The output of this command informs Paul that he may execute only shutdown -r (just like Mary said). Notice that it also informs him that he may run all commands in /usr/local/db/bin/, as well as the commands /usr/sbin/lpc and /usr/bin/lprm as either the root or dcmgr users. However, he cannot

### Example 9-7 Failed sudo Execution Due to Incorrect Command

```
[paul@fohgnrn]$ sudo /sbin/shutdown now
Password:
Sorry, user paul is not allowed to execute "/sbin/shutdown now" as root on fohgnrn.
[paul@fohgnrn]$ 
```
