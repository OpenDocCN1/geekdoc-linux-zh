
## Add-On Postfix

An *add-on postfix* instructs the server to append one or more characters to the end of a filename during the transfer or reception of a file. A server can contain TARed packages of applications that are uncompressed. If an add-on postfix conversion is configured on the server, the server could compress the file, append a .gz extension after the file was compressed, and then send that file to the client. The server could also perform the same action for uncompressed files sent to the server. This would have the effect of conserving disk space on the server.

## External Command

The *external command* entries in the `ftpconversions` file contain the bulk of the FTP server conversion rules. The external command entry tells the server what should be done with a file after it is transferred to the server. The specified conversion utility can be any command on the server, although generally it is a compression utility. As the file is sent, the server passes the file through the external command. If the file is being uploaded to the server, the command needs to send the result to standard in, whereas a download sends the result to standard out. For example, here is an entry specifying the tar command:

```
::tar:/bin/tar -c -f - %s:T_REG|T_DIR:O_TAR: TAR
```

The following sections describe the fields in a conversion entry.

### Types

You must use the *types* field of the `ftpconversions` file to tell the server to what types of files the conversion rules apply. Separate the file type entries with the (|) character, and give each *type* a value of `T_REG`, `T_ASCII`, and `T_DIR`.

`T_REG` signifies a regular file, `T_ASCII` an ASCII file, and `T_DIR` a directory. A typical entry is `T_REG | T_ASCII`, which signifies a regular ASCII file.

### Options

The *options* field informs the server what action is being done to the file. Similar to the *types* field, options are separated by the (|) character. Here are the valid ranges you can assign to items in the *options* field:

- `O_COMPRESS` to compress the file
- `O_UNCOMPRESS` to uncompress the file
- `O_TAR` to tar the file

An example of this field is `O_COMPRESS | O_TAR`, where files are both compressed and TARed.

### Description

The description field allows an administrator to quickly understand what the rule is doing. This field does not have any syntax restriction, although it is usually a one-word entry—such as **TAR**, **TAR+COMPRESS**, or **UNCOMPRESS**—which is enough to get the concept across.

### An Example of Conversions in Action

Crafting complex conversion entries is a task perhaps best left to the Linux/Unix expert, but the sample **ftpconversions file** included with **wu-ftpd** provides more than enough examples for the average Red Hat administrator. Building your own simple conversion entry is not really too difficult, so let’s examine and decode an example:

In this example, the strip prefix (field 1) is **null** because it is not yet implemented, so this rule does not apply to prefixes. The second field of this rule contains the `.Z` postfix; therefore it deals with files that have been compressed with the **compress** utility. The rule does not address the add-on prefix or postfix, so fields 3 and 4 are **null**. Field 5, the external command field, tells the server to run the **compress** utility to decompress all files that have the `.Z` extension, as the `-d` parameter signifies. The `-c` option tells **compress** to write its output to standard out, which is the server in this case. The `%s` is the name of the file against which the rule was applied. Field 6 specifies that this file is a regular file in ASCII format. Field 7, the options field, tells the server that this command uncompresses the file. Finally, the last field is a comment that gives the administrator a quick decode of what the conversion rule is doing—that is, uncompressing the file.

### Examples

Several conversion rules may be specified in **wu-ftpd**’s default **ftpconversions** file. Additional examples of conversion rules, such as for Sun’s Solaris operating system, might be available in the **wu-ftpd** documentation.

## Using ftphosts to Allow or Deny FTP Server Connection

The purpose of the **ftphosts** file is to allow or deny specific users or addresses from connecting to the FTP server. The format of the file is the word **allow** or **deny**, optionally followed by a username, followed by an IP or a DNS address.

```
allow username address
deny username address
```

Listing 20.3 shows a sample configuration of this file.

**LISTING 20.3 ftphosts Configuration File for Allowing or Denying Users**

```
# Example host access file
#
# Everything after a '#' is treated as comment,
# empty lines are ignored
allow tdc 128.0.0.1
allow tdc 192.168.101.*
allow tdc insanepenguin.net
allow tdc *.exodus.net
deny anonymous 201.*
deny anonymous *.pilot.net
```

The `*` is a wildcard that matches any combination of that address. For example, `allow tdc *.exodus.net` allows the user `tdc` to log in to the FTP server from any address that contains the domain name `exodus.net`. Similarly, the `anonymous` user is not allowed to access the FTP if he is coming from a 201 public class C IP address.

Changes made to your system's FTP server configuration files become active only after you restart `xinetd` because configuration files are parsed only at startup. To restart `xinetd` as root, issue the command `/etc/rc.d/init.d/xinetd restart`. This makes a call to the same shell script that is called at system startup and shutdown for any runlevel to start or stop the `xinetd` daemon. `xinetd` should report its status as:

```bash
# /etc/rc.d/init.d/xinetd restart
Stopping xinetd: [  OK  ]
Starting xinetd: [  OK  ]
```

When the FTP server restarts, it is accessible to all incoming requests.

## Using Commands for Server Administration

`wu-ftp` provides a few commands to aid in server administration. Those commands are:

- **ftpwho**—Displays information about current FTP server users
- **ftpcount**—Displays information about current server users by class
- **ftpshut**—Provides automated server shutdown and user notification
- **ftprestart**—Provides automated server restart and shutdown message removal

Each of these commands must be executed with superuser privileges because they reference the `ftpaccess` configuration file to obtain information about the FTP server.

## Display Information About Connected Users

The `ftpwho` command provides information about the users currently connected to the FTP server. Here's the command line:

```
/usr/bin/ftpwho
```

Table 20.3 shows the format of the output `ftpwho` displays.

**TABLE 20.3 ftpwho Fields**

| Name | Description |
| :--- | :--- |
| Process ID | The process ID of the FTP server process. |
| TTY | The terminal ID of the process. This is always a question mark (?) because the FTP daemon is not an interactive login. |
| Status | The status of the FTP process. The values are: S: Sleeping, Z: Zombie, indicating a crash, R: Running, N: Normal process. |
| Time | The elapsed processor time the process has used in minutes and seconds. |
| Details | Tells from what host the process is connecting, the user who connected, and the currently executing command. |

Listing 20.4 shows typical output from this command. It lists the process ID for the ftp daemon handling requests, the class to which the particular user belongs, the total time connected, the connected username, and the status of the session.

In addition to the information given about each connected user, ftpwho also displays the total number of users connected out of any maximum that has been set in the ftpaccess file. This information can be used to monitor the use of your FTP server.

You can pass one parameter to ftpwho. (You can find the parameter by using the ftpwho -help command.) The single parameter you can pass to ftpwho is -v. This parameter prints out version and licensing information for wu-ftp, as shown here:

```
# ftpwho
Service class all:
10447 ? Sn 0:00 ftpd: localhost: anonymous/winky@disney.com: IDLE
1 users (no maximum)
```

The output of ftpwho, using the -V option, which shows version information, is shown in Listing 20.4.
