
Syntax: chmod yes|no typelist
Default: chmod no guest,anonymous

![](img/9eb7e89292d2f85707b4d49102c865b7_433_0.png)

The chmod command is not available by default.

### delete

This keyword enables or disables the delete (del) command for users specified in the type list. For example, the default setting disables the delete command for both guest and anonymous users.

Syntax: delete yes|no typelist
Default: delete no guest,anonymous

### overwrite

This keyword enables or disables the overwriting of files by the users specified in the typelist. For example, the default setting disables file overwriting for both guests and anonymous users.

Syntax: overwrite yes|no typelist
Default: overwrite no guest,anonymous

### rename

This keyword enables or disables the rename command for specified users in the typelist. For example, the default setting disables the rename command for both guest and anonymous users.

Syntax: rename yes|no typelist
Default: rename no guest,anonymous

### umask

This keyword enables or disables the umask command (site umask) for specified users in the typelist.

Syntax: umask yes|no typelist

![](img/9eb7e89292d2f85707b4d49102c865b7_433_1.png)

The umask command is not available by default.

### passwd-check

This keyword defines the type of passwords required for anonymous users. The default setting requires the password for an anonymous access to be an e-mail address but does not enforce this rule if the user fails to enter a valid e-mail address. The server just warns the user about the invalid password.

**Syntax:** `passwd-check none|trivial|rfc822 (enforce|warn)`

**Default:** `passwd-check rfc822 warn`

When you don’t want password checking, set the passwd-check keyword as follows:

```
passwd-check none
```

If you set the checking to be trivial, the server checks only for the existence of an @ character in the password.

### path-filter

This keyword enables you to restrict certain filenames, specifically those used in file uploads by users specified in typelist.

**Syntax:** `path-filter typelist mesg allowed_charset {disallowed regexp . . .}`

### upload

This keyword allows you to enable or disable an upload directory.

**Syntax:** `upload root_dir dirglob yes|no owner group`

For example, the following directive enables the /dropbox directory as an upload directory where files are owned by root and the group ownership is set to ftp:

```
upload /home/ftp /dropbox yes root ftp 0600
```

The uploaded files have a permission setting of 0600. Note that /home/ftp must be the home directory of the user ftp. If the uploader should not be allowed to create new subdirectories under the /dropbox directory, then the preceding upload line needs to be changed to:

```
upload /home/ftp /dropbox yes root ftp 0600 nodirs
```

On the other hand, if the uploader should be allowed to create subdirectories, then nodirs can be replaced with dirs.

## Miscellaneous configuration

The following keywords allow you to control miscellaneous settings.

### alias
This keyword enables you to create an alias for a directory.

**Syntax:** `alias string dir`

For example, the following allows a user to type the cd redhat command to change to /pub/linux/distributions/redhat directory:

```
alias redhat /pub/linux/distributions/redhat
```

### cdpath
This keyword adds the specified directory to the search path of the change directory (cd) command.

**Syntax:** `cdpath dir`

For example:

```
cdpath /pub/linux/redhat
```

Now if a user enters the command cd RPMS, the server first looks for a directory called RPMS in the user's current directory. If it fails to find one, it looks for an alias called RPMS, and if it fails to find an alias RPMS, then it tries to change directory to /pub/linux/redhat/RPMS.

### compress
This keyword enables or disables the compression feature for specified classes.

**Syntax:** `compress yes|no class [class ...]`

**Default:** `compress yes all`

The default setting allows the compression feature for the class called all, which by default covers all real, anonymous, and guest users. When the default is left alone and the ftpconversions file is not modified, all the users who use the FTP service are able to compress files on the fly. For example, a user who wants to get the entire contents of a directory as a compressed file can enter the get directoryname.tar.gz command, and a compressed tar file is downloaded.

### tar
This keyword enables or disables the tar (tape archive file) feature for specified classes. The default setting allows the compression feature for the class called all, which by default covers all the real, anonymous, and guest users. When the default is left alone and the ftpconversions file is not modified, all the users who use the FTP service are able to tar files on the fly.

Syntax: tar yes|no class [class ...]

Default: tar yes all

For example, a user who wants to get the entire contents of a directory as a compressed file can enter the get directoryname.tar command to download a tar file.

## shutdown

This keyword specifies the file that the FTP server monitors from time to time to detect a shutdown event. You can create this file using the ftpshut command.

Syntax: shutdown path

Default: shutdown /etc/shutmsg

For example, to shut down the server immediately, you run the following command:

```
ftpshut now
```

However, you can schedule a shutdown in such a way that the logged-in users have some time before the shutdown begins. For example, say the current date is Monday, December 13, 1999, and the time is 1600 (in 24-hour format). To shut down the system in an hour, you can use the following command:

```
ftpshut -d 30 1700
```

This creates the /etc/shutmsg file as follows:

```
1999 11 13 17 00 0010 0030
System shutdown at %s
```

The format of the first line is as follows:

```
YYYY MM DD HH MM HHMM HHMM
```

The YYYY is the year, MM is the month (0-11), DD is the day (1-31), HH is the hour (0-23), and MM is the minute (0-59). The first HHMM pair is the offset in time for denying new connections, and the second HHMM pair is the offset in time for disconnecting current connections. As you can see, the –d 30 option set the last HHMM pair to 0030 in the example file just shown. The deny offset for new connections by default is 10 minutes, but you can change that with –l option. Also note that you can supply a more customized warning message than the default System shutdown at %s using one or more of the magic cookies shown in Table 14-3.

## Table 14-3 Magic Cookies for FTPSHUT Warning Message

| Magic Cookie | Replacement Text |
|---|---|
| %s | The time the system is going to shut down |
| %r | The time new connections will be denied |
| %d | The time current connections will be disconnected |

In addition to these cookies, you can use all the cookies shown in Table 18-2. To create such a message, run the ftpshut command as follows:

```
ftpshut -d MM -l MM HHMM "Shutdown at %s. Be done by %d."
```

Don't forget to replace the MM, HHMM, and so on with appropriate values. Also note that when you are ready to restart the FTP service, you have to remove the /etc/shutmsg file.

### virtual
If you have multiple IP addresses for your Linux system and would like to offer virtual FTP services, you can use this keyword. See the “Creating virtual FTP sites” section later in this chapter for details.

```
Syntax: virtual address root|banner|logfile path
```

## /etc/ftpconversions

The /etc/ftpconversions file stores the FTP server's conversion database. The default configuration for this file is sufficient for almost all install-ations. If you need more information, see the man page for ftpconversions.

## /etc/ftpgroups

The file /etc/ftpgroups is important only if you allow the nonstandard SITE commands. The wu-ftpd package that ships with Red Hat Linux comes with the SITE commands disabled. This is done to enhance security, as SITE commands have been known to create security holes in earlier versions of the server. For the sake of completeness, I describe the purpose of this file, but I strongly discourage its use.

When a not-so-security-savvy FTP administrator enables the SITE commands, she needs to set up the /etc/ftpgroups file as follows:

```
groupname:encrypted password:realgroup
```

Typically, the SITE GROUP and SITE GPASS commands are used to allow an already-logged-in FTP user to upgrade her group privileges. The /etc/ftpgroups file provides the necessary mapping for a user of groupname to be upgraded to the realgroup when a valid password is entered by using the SITE GPASS command. Also note that the realgroup must be a group in the /etc/group file.

## /etc/ftphosts

The file /etc/ftphosts is used to control FTP access to specific accounts from various hosts. To allow a user to log on from one or more hosts, use a line such as the following:

```
allow username addrglob [addrglob...]
```

This command allows the specified user to log on from the specified hosts. For example:

```
allow joegunchy *.evoknow.com
```

Here the user joegunchy is allowed to log on from any machine in the evoknow.com domain. To deny a user the ability to log onto the server from one or more hosts, you can use the following line:

```
deny username addrglob [addrglob...]
```

For example, to prevent joegunchy from logging into the server from the 206.171.50.0 network, you can use the following command:

```
deny joegunchy 206.171.50.*
```
