
## Example 9-8 Using sudo -l

```
[paul@foghorn]$ sudo -l
You may run the following commands on this host:
        (root, dbmgr) /usr/sbin/lpc; /usr/bin/lprm
        (root, dbmgr) /sbin/shutdown -r *
        (root, dbmgr) /usr/local/db/bin/
[paul@foghorn]$
```

execute /sbin/shutdown -r as dbmgr. This is simply due to the fact that running the shutdown command as a user other than root will always result in permission denied.

Now that he knows which command it is, he executes it successfully, as indicated, in Example 9-9. The moral of this story is that the command executed through sudo must match *exactly* that given in /etc/sudoers or as displayed by sudo -l.

## Example 9-9 Successful sudo /usr/sbin/shutdown -r Invocation

```
[paul@foghorn]$ sudo /sbin/shutdown -r now
Broadcast message from root (tty0) Wed Mar 10 06:55:39 1999...
        The system is going down for reboot NOW !!
```

## OH, BY THE WAY...

Since we compiled sudo with insults (see Example 9-1 on page 177), let's have a look at what that means. In Example 9-10, we show the user paul mistyping his password twice.

Without the --with-insults compile-time option, whenever you enter an incorrect password, you would simply see the message, Sorry, try again. The UNIX operating system used to be full of humorous, insulting, and sometimes offensive error messages. As it has become more commercialized, most of these messages have been sanitized. So, harken back to the days of yore, and compile with insults!

## Example 9-10 Insulting Error Messages

```
[paul@foghorn]$ sudo /sbin/shutdown
Password:
        Listen, burrito brains, I don't have time to listen to this trash.
Password:
        Your mind just hasn't been the same since the electro-shock, has it?
Password:
        Sorry, user paul is not allowed to execute "/sbin/shutdown" as root on foghorn.
[paul@foghorn]$
```

## General Syntax of /etc/sudoers

Now that we have explored some relatively simple examples associated with the /etc/sudoers file, let's take a look at the full suite of capabilities. The file is broken into two major sections, the alias section and the privilege section. The alias section in the file is largely for convenience. It is the privilege section of the file that actually avails a particular user of root permissions. Table 9.2 describes the alias options available to this file.

### Table 9.2 Alias Syntax for /etc/sudoers

| Alias Type | Required Keyword | Alias Syntax | Description |
|---|---|---|---|
| Host_Alias | | HOSTALIAS= | Comma-separated list of hostnames, IP addresses, network/netmask, and/or netgroups. |
| Runas_Alias | | RUNASALIAS= | Comma-separated list of users, groups, and/or net-groups. Specifies UIDs that will be accepted by sudo -u. |
| Cmnd_Alias | | CMNDALIAS= | Comma-separated list of commands or directories. Must be absolutely qualified. When a command is specified, flags and arguments may also be specified. The special characters `*` and `?`, when given as a command argument means that no arguments are allowed. Thus, do not quote commands! When a directory is specified, it includes all commands in that directory. |
| User_Alias | | USERALIAS= | Comma-separated list of users, groups, and/or netgroups. |

¹Netgroups are groups of (host, user, domain) triples often used for permission checking over the network. See the references noted in NFS, Samba, NIS, and DNS Resources on page 40.

In our earlier examples, we did not look at the Host_Alias capability. By using this alias type, we can configure a /etc/sudoers file for all the systems in a given environment. It may even be shared via NFS or distributed to multiple systems through the `rdist` or `rsync` utilities.¹

We also did not explore the Runas_Alias capability. This alias, as described in Table 9.2, simplifies the process of specifying the users for which sudo will run as, since it assume the real and effective UID of the indicated user.

The privilege specification takes the syntax shown in Example 9-11. While this syntax appears to be very complex at first glance, it is actually quite straightforward. We have already seen some simple examples of this syntax in use in Example 9-4 on page 179. This representation points out the full capabilities of the entries in /etc/sudoers. Table 9.3 helps to illustrate the various types shown in Example 9-11. We will look at the further implementation of this syntax in A More Sophisticated Example on page 185.

## Example 9-11 Syntax of Privilege Entries in /etc/sudoers

```text
access_group host_type = {runas_type,runas_type,...} {NOPASSWD:} \
[{!}cmd_type[{runas_type,...}]{, [NOPASSWD:} \
[{!}cmd_type[{runas_type,runas_type,...}]], {,...} }
{host_type=[...]}
```

1. These utilities allow for automated distribution of file(s) to various hosts. See your system documentation for the proper use of `rdist` and `rsync`.

| Parameter | Description |
|---|---|
| access_group | A user, %group, +netgroup, or USERALIAS. |
| host_type= | A host, IP address, +netgroup, network/netmask, or HOSTALIAS. The = must follow with no white space. |
| (runas_type) | A user, %group, +netgroup, or RUNASALIAS. The parentheses are required. |
| cmd_type | A command or CMDALIAS. |
| NOPASSWD: | No password is required for the command following this keyword. A space is required after the NOPASSWD :. |
| ! | The logical NOT operator. Only applied to cmd_type. |
| : | This separator follows a cmd_type and precedes a host_type = with no intervening white space. |
| ALL | Special keyword that expands to all of the given type. |

There are also metacharacters that may be used in this file. The wildcard and escape characters are defined identically to their shell counterparts. They are described in Table 9.4.

As you might imagine, the /etc/sudoers file can get quite complex. A modestly complex example is given in Example 9-12 on page 185. Also in the section Vulnerabilities of sudo on page 191, some of the vulnerabilities associated with misconfiguring the /etc/sudoers file are described. It turns out that,

| Metacharacter | Description |
|---|---|
| * | Matches 0 or more characters. |
| ? | Matches exactly 1 character. |
| [range,range,...] | Matches any character in the range. |
| [!range,!range,...] | Matches any character not in the range. |
| \ | Escapes the next character. |
| “” | The null string. Used to indicate that no arguments or flags may be passed to a command. |
| # | Comment character. Any text after this character is ignored. |
| % | Specifies a UNIX group such as %wheel. |
| + | Specifies a netgroup such as +admins. |

if an `/etc/sudoers` file has a syntax error in it, `sudo` won't work at all. For this reason, the `visudo` command is included with `sudo` distribution.

## The visudo Command

Only root can execute `visudo`. However, this also means that any user with the appropriate permissions can execute `sudo visudo` (remember, `sudo` sets both the real and effective UID to 0). By default, `visudo` invokes the `vi` editor (this may be changed with the `-with-editor` option to `configure`) and when editing is complete (that is, a save operation is effected, such as “:wq”), `visudo` does a syntax check before saving the file. If there are syntax errors in the file, `visudo` will give you the option to read it the file, quit without saving the changes, or quit and save the changes. Be warned that if you save syntax errors, `sudo` will not work.

## Options to the sudo Command

Table 9.5 explains the available options to `sudo`. Remember that use of `sudo` is completely controlled by the `/etc/sudoers` file.

### Table 9.5 Options to sudo

| Option | Description |
| :----- | :-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| -v | Prints the version and quits. |
| -h | Prints the usage message and quits. |
| -1 | Lists the allowed and forbidden commands for the invoking user. |
| -v | Validates the user: This command will reset the timestamp for the invoking user in `/var/run/sudo`. If the time-out has already occurred, it will prompt the user for a password. |
| -k | Removes the user's timestamp file, forcing the user to respond to the password prompt at the next invocation of `sudo`. This option never requires a password and may be put in the user's `.logout` file. |
| -s | Executes the shell specified by the `SHELL` environment variable or, if not set, the user's default shell as found in `/etc/passwd`. Beware! Any commands executed after the successful invocation of `sudo -s` are not logged! This command is similar to `sudo /path/to/shell`. |
| -H | Sets the `HOME` environment variable to that of the target user, which is root by default, but will assume `$HOME` of target user if `-u` option is specified. |
| -b | Puts the command in the background. Using this option disables shell job control. You may wish to specify `&` at the end of the command instead. |
