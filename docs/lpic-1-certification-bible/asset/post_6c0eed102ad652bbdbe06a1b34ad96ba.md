
The most popular FTP server is still **wu-ftpd**, but **ProFTPD** is a popular new alternative. ProFTPD has a similar configuration structure to Apache.

The most popular FTP server is wu-ftpd, created by Washington University. It is included with most Linux distributions. The `ftpd` daemon is normally run by `inetd` and enabled through the `/etc/inetd.conf` file. The following line shows the appropriate entry:

```text
ftp     stream    tcp     nowait    root    /usr/sbin/tcpd -l -a
```

The `ftpd` daemon takes the parameters shown in Table 16-2.

### Table 16-2
### ftpd Parameters

| **Parameter** | **Function** |
| :--- | :--- |
| -V | Display version information. |
| -d | Write debug information to `syslog`. |
| -v | Write debug information to `syslog`. |
| -l | Log connections to `syslog`. |
| -t <value> | Set the amount of time a client may be idle before being disconnected. |
| -a | Use the `ftpaccess` configuration file. |
| -A | Do not use the `ftpaccess` configuration file (default). |
| -L | Log all user commands to `syslog`. |
| -I | Log received files to `xferlog`. |
| -i | Enable checking of the client name via `ident`. |
| -O | Log transferred files to `xferlog`. |
| -X | Log -i and -o information to `syslog` to facilitate central logging. |
| -W | Do not log logins to `wtmp`. |
| -r | Chroot (change root) the daemon as soon as it loads, not at login. This changes the perceived root directory for the daemon. For example, if you chroot the daemon to `/var/ftp`, the daemon will use that as its root. If someone breaks in to your FTP server they can not go below that directory. |

# Setting up anonymous FTP

Configuring anonymous FTP requires a few steps. Some Linux distributions automatically install and set up the server to allow anonymous access. The following steps walk you through setting it up manually and show you how it was done if your distribution did it for you.

- 1. Create a user named "ftp".
- 2. Create the following subdirectories under the ftp user's home directory: bin, etc, lib, and pub.
- 3. Copy any needed binaries to the bin directory. These may include ls, more, gzip, and tar.
- 4. Copy any needed library files for the binary files to the new lib directory.
- 5. Copy /etc/passwd and /etc/group to the new etc directory.
- 6. Edit the /etc/passwd file and change any encrypted passwords to asterisks.
- 7. Set the directory permissions as shown in Table 16-3.

When a user logs in via anonymous FTP, the server changes their perceived root, known as chroot, to the ftp user's home directory. The newly created directories are needed to provide any files a user may need.

### Table 16-3
### Permissions

| File/Directory | Owner/Group | Permissions |
|---|---|---|
| ~ftp | root/root | 555 (r-xr-xr-x) |
| ~ftp/bin | root/root | 555 (r-xr-xr-x) |
| ~ftp/bin/<file> | root/root | 111 (--x--x--x) |
| ~ftp/etc | root/root | 555 (r-xr-xr-x) |
| ~ftp/etc/passwd | root/root | 444 (r--r--r--) |
| ~ftp/etc/group | root/root | 444 (r--r--r--) |
| ~ftp/pub | root/ftp | 755 (rwxr-xr-x) |
| ~ftp/lib | root/root | 755 (rwxr-xr-x) |
| ~ftp/lib/<file> | root/root | 755 (rwxr-xr-x) |

For the sake of security, it is a good idea to remove unneeded users from the /etc/passwd file when copying it to the ~ftp/etc directory. Only the ftp, daemon, and root users need to be in the file. This way an anonymous user cannot get a list of user accounts on the machine to aid in hacking. It is also recommended to set the ftp user's shell to /bin/false, so there is no way for the user to Telnet or log in remotely.

> The anonymous FTP account should not have a valid shell statement in /etc/passwd. The /bin/false entry is normally used. Whatever fake statement is used, it must be present in the /etc/shells file.

# Customizing configuration files

The wu-ftpd server provides several configuration files to control access to the server and other options. These are the following:

- /etc/ftpaccess
- /etc/ftphosts
- /etc/ftpusers
- /etc/ftpgroups
- /etc/ftpconversions
- /var/log/xferlog

Most of these files are already configured to work with an anonymous server during the Linux distribution install. Only when the service is expanded do you need to edit these.

# The ftpaccess file

The ftpaccess file can be used to set restrictions, logging, information, and other options on the FTP server. An example ftpaccess file is shown here:

```
class all real,guest,anonymous *

email Jason@the-nashes.net

loginfails 5

readme README* login

readme README* cwd=* 

message /welcome.msg login

message .message cwd=* 

compress yes all

tar yes all

chmod no guest,anonymous

delete no guest,anonymous

overwrite no guest,anonymous

rename no guest,anonymous

log transfers anonymous,real inbound,outbound

shutdown /etc/shutmsg
passwd-check rfc822 warn
```

Table 16-4 shows the common ftpaccess entries.

### Table 16-4
### Common ftpaccess Entries

| Information Entries | Function |
| :------------------ | :------- |
| banner `<file>` | The specified text file is displayed when a user connects, before their user name or password is entered. The full path from the volume root is required. |
| message `<file>` {`<when>` {`<class>` ...}} | The file defined in the `<file>` is displayed to the client when specified. The `<when>` parameter can either be LOGIN, to display at login, or CWD=`<directory>`, to display the file when a user changes into the defined directory. Variables known as “Magic Cookies” can be put in the text file to have the FTP server replace them with other information. See the man page for more information. |
| email `<email address>` | Defines the administrator’s e-mail address that can be referenced with a “Magic Cookie.” |
| readme `<path>` {`<when>` {`<class>`}} | Displays a message telling the user when the file specified in `<path>` was modified. This is useful for a README file containing important information and for informing users of updates. |
| **Access Control** | **Function** |
| autogroup `<group name>` `<class>` {`<class>`...} | If the anonymous FTP user is a member of any defined `<class>`, that user’s group is changed to `<group name>`. |
| class `<class>` `<typelist>` `<address glob>` {`<address glob>`...} | Defines a `<class>` of users based on their `<address glob>`. The `<typelist>` defines the user type as anonymous, guest, and real. The groups of users are then referenced elsewhere in the ftpaccess file to make administration easier. |
| | The `<address glob>` is either a domain name or a numeric address, such as 192.168.1.*. |
| deny `<address glob>` `<message file>` | Displays the `<message file>` to any address matching the `<address glob>` and then denies access. |
| limit `<class>` `<n>` `<times>` `<message_file>` | Limits the `<class>` to `<n>` number of users connected during `<times>`. If the limit is reached the `<message_file>` is displayed. |
| noretrieve [absolute\|relative] [class=<classname>] ... [-] `<file name>` ... | Blocks the retrieval of certain files. Paths can be set to either absolute or relative, and restricted by class. This is useful for blocking the downloading of the /etc/passwd file. |
| allow-retrieve [absolute\|relative] [class=<classname>]... [-] `<filename>` ... | Allows files to be retrieved that would normally be blocked by the noretrieve entry. |
| loginfails `<number>` | After `<number>` of attempts to enter the correct password, the FTP connection is disconnected. |
| private `<yes\|no>` | Allows the user to change to a different group using the SITE GROUP and SITE GPASS commands. The group must be specified in the /etc/ftpgroups file. |
| **Logging** | **Function** |
| log commands `<typelist>` | Logs commands for user types specified in `<typelist>`. These are real, anonymous, and guest. |
| log transfers `<typelist>` `<directions>` | Logs transfers by `<typelist>`. `<directions>` are either inbound or outbound. |
| log security `<typelist>` | Logs security violations for the user type specified in `<typelist>`. The violations are things such as trying to download files protected by noretrieve. |
| **Miscellaneous Capabilities** | **Functions** |
| alias `<string>` `<dir>` | Creates an alias that refers to a directory. Used only by the cd command. |
| cdpath `<dir>` | Defines a search path for directories. If a user should enter cd foo, the current directory and those listed with cdpath will be checked. |
| compress `<yes\|no>` `<classglob>` ... | Enables the compress function so files can be shrunk before downloading. |
| tar `<yes\|no>` `<classglob>` ... | Enables the tar function. |
