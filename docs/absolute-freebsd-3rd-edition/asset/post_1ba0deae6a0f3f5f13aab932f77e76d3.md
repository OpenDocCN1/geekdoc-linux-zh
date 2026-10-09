
# **User Accounts and Root Password**

You can add user accounts and change passwords only from within the jail. Set a root password with `passwd(1)` and run `adduser(8)` to add at least one user, for SSH. While SSH is not the only way to access the host, it’s far easier in most cases.

## Jail Startup and Shutdown

The host considers each jail an independent service, much like `sshd(8)`, a web server, or any other daemon. Yes, each jail might run a whole bunch of services that need managing independently, but from the host’s perspective, each jail is a single entity containing a group of processes. That’s part of the separation between the host and the jail.

Use `service(8)` to start, stop, and restart jails. You’ll need to provide one additional argument, the name of the jail. FreeBSD automatically starts them at boot, but you can stop, start, and restart them individually once the system is running. Let’s shut down my database jail and fire it up again.

```
# service jail stop mariadb
# service jail start mariadb
```

I could use the restart command, but that wouldn’t look nearly so impressive here on the page.

If you omit the jail name, the `service(8)` command affects all jails that FreeBSD starts at boot.

```
# service jail restart
Stopping jails: httpd mariadb.
Starting jails: mariadb httpd
```

This lets you coherently reinitialize your production jail infrastructure.

FreeBSD defaults to starting all jails listed in `/etc/jail.conf`. As discussed in “Jails at Boot” on page 568, you can change that in `/etc/rc.conf`. The `service(8)` command can control jails that aren’t autostarted, but you must specify them by name.

## Jail Dependencies

If you have a whole bunch of jails, listing the start order in `/etc/rc.conf` can get tedious. You’ll most often need to set a start order to maintain service dependencies. Rather than defining the order in `rc.conf`, though, you can tell a jail that it requires another jail with the `depend` option.

```
httpd {
    ip4_addr="203.0.113.232";
    depend=mariadb;
}
```

The jail `httpd` won’t start until the jail `mariadb` is running. A `depend` statement overrides a `rc.conf` `jail_list` entry.

## Managing Jails

Virtualization doesn’t make system administration tasks evaporate; it only adds options for performing typical sysadmin tasks. Here’s some of those options.

### Viewing Jails and Jail IDs

Use `jls(8)` to see all jails currently running on the system.

```
# jls
 JID  IP Address     Hostname            Path
  29  203.0.113.221  mariadb.mwl.io      /jail/mariadb
  30  203.0.113.222  httpd.mwl.io        /jail/httpd
  31  203.0.113.223  test.mwl.io         /jail/test
```

Each jail has a unique jail ID, or JID. The JID is much like a process ID; while each jail has one, the exact JID issued to a jail changes each time the jail is started. We’ll use the jail ID or name to execute various jail-management tasks.

We also get each jail’s IP address, hostname, and the path to the jail’s files. You don’t get the jail name, but those of us who use a hostname based on the jail name have no trouble figuring it out.

## Jailed Processes

Jailed processes all get a process ID, like any other Unix process. Process IDs are not unique to jails; they’re shared between the host, the jail, and all the other jails. You won’t find repeated process IDs.

Jailed processes show up in `ps(1)` with the `-j` flag.

```
# ps -ax
PID  TT  STAT     TIME  COMMAND
  0   -  DLs      2:56.24 [kernel]
  1   -  ILs      0:00.07 /sbin/init -
--snip--
35002 -  SsJ      0:00.01 /usr/sbin/syslogd -s
35129 -  IsJ      0:00.00 /usr/sbin/sshd
--snip--
```

Process IDs 35002 and 35129 are jailed.

View a particular jail’s processes with `ps(1)` using the `-j` flag and the jail name.

```
# ps -ax -J test
PID  TT  STAT     TIME  COMMAND
35561 -  IsJ      0:00.01 /usr/sbin/syslogd -s
35652 -  IsJ      0:00.00 /usr/sbin/sshd
35661 -  SsJ      0:00.03 sendmail: accepting connections (sendmail)
--snip--
```

Using `-j 0` excludes all jailed processes from `ps(1)` output, letting you more easily debug the host.

Commands like `pgrep(1)`, `pkill(1)`, and `killall(1)` all accept a `-j` argument to let you specify a jail. If you prefer using `pgrep(1)` to view process information, use `pgrep -lfj` and the jail name or JID.

```
# pgrep -lf -J mariadb
PID  TT  STAT     TIME  COMMAND
35002 -  SsJ      0:00.01 /usr/sbin/syslogd -s
35129 -  SsJ      0:00.00 /usr/sbin/sshd
35158 -  SsJ      0:00.02 sendmail: accepting connections (sendmail)
--snip--
```

Why is Sendmail running inside this jail? Let’s kill it.

```
# pkill -9 -J mariadb sendmail
```

Running `pgrep` again shows that Sendmail is dead.

This works well if you want to get information about which processes are running in a jail, but sometimes you have a process ID and must identify which jail it belongs to. That's where you need the `-o` option to `ps(1)`. This option supports a bunch of keywords that adjust the output of `ps(1)` in ways not supported by the regular command line flags—specifically, `-o jail` adds a column for the name of the jail the process is running in.

```
# ps -ax -o jail | grep 39415
39415 mariadb - IsJ 0:00.00 /usr/local/libexec/mysql
```

This process is running inside the jail `mariadb`.

# **Running Commands in Jails**

The `jexec(8)` command lets the jail host administrator execute commands within a jail without going to the trouble of logging into the jail. This helps preserve the jail owner's sense of privacy. When jail owner Bert calls to beg for help, I don't need his root password or even an account on his system. Using `jexec` requires knowing the jail's name or JID. Here, I use the host's root account to run `ps -ax` inside my jail `mariadb`.

```
# jexec mariadb ps -ax
PID TT STAT TIME COMMAND
35002 - SsJ 0:00.00 /usr/sbin/syslogd -s
35129 - IsJ 0:00.00 /usr/sbin/sshd
--snip--
```

This command runs as root inside the jail. I might want to run the command as another jailed user, though. Give that username with the `-u` flag.

```
# jexec -U xistence mariadb ps
jexec: xistence: no such user
```

Well, that's not good. I'm expecting Bert to run my database. Let's make him a user account.

```
# jexec mariadb adduser
Username: xistence
Full name: Bert JW Regeer
Uid (Leave empty for default):
Login group [bert]:
Login group is bert. Invite bert into other groups? []: wheel
--snip--
```

This jail now has an account for Bert, using his preferred username and everything. I've added it to the wheel group within the jail. Remember, root access within a jail doesn't equal root access on the host. That's the whole point of jails.
I can now run commands as that user in that jail.

```
# jexec -U xistence mariadb sh
$ 
```

I'm locked up in jail! Specifically, in Bert's jail cell.
This jailed process will behave a little oddly, though. A process retains its environment. In this case, while I'm running as the user xistence, I retain all the environment settings I had in my nonjailed process. This includes stuff like $SSH_AUTH_SOCK, my IRC server setting, and more. I don't want this stuff in my jailed environment. If I'm logged in as Bert, I want to be Bert.
To strip your environment before entering a jail, use jexec's -1 flag. This simulates a clean login.

```
# jexec -lU xistence mariadb sh
```

Should you always strip your environment before running a command in a jail? No, not always. It depends entirely on what you're doing.
Many commands include support for running them on the host but targeting a jail. Always check the man page for such an option. One good example is `sysrc(8)`, which lets you specify a jail with `-j`. Here, I enable MariaDB on the jail `mariadb`. MariaDB has chosen to continue to use MySQL naming conventions, so it's enabled with the `rc.conf` option `mysql_enable`.

```
# sysrc -j mariadb mysql_enable=YES
mysql_enable:  -> YES
```

This jail is now ready to run MariaDB.
Except for the bit where MariaDB isn't installed, of course. Let's take care of that next.

### *Installing Jail Packages*

FreeBSD's package tools let you manage software either from within the jail or from the host. If the host administrator has allocated you a jail to configure, you probably want to manage packages from the jail. Jail packages work exactly as packages on any other FreeBSD host, as discussed in Chapter 15. If you're responsible for the whole system, including the host and all the jails on that host, you probably want to manage each jail's packages from the host rather than logging into each jail. Let's spend some time on that.

The `pkg(8)` command's `-j` flag lets you specify a jail to manage. You'll need one argument, the jail's name or JID. The `-j` flag must be given before the `pkg(8)` subcommand. Here, I install the MariaDB server on its dedicated jail:

```
# pkg -j mariadb install mariadb101-server
Updating FreeBSD repository catalogue...
FreeBSD repository is up to date.
All repositories are up to date.
The following 9 package(s) will be affected (of 0 checked):
--snip--
```

Note that `pkg(8)` offers no notice that it's installing packages within a jail. It assumes that if you're using `-j`, you know you're working in a jail.
When you manage a jail's packages from the host, the package tools don't get installed on the jail. The jail has its own package database, stored within the jail, but the jail has no way to use that database directly.
Don't switch between managing packages on the host and from within the jail. Choose one method and stick with it.
