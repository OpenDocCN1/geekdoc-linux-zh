
## TABLE 23.4 Magic Cookies for the ftpshut Command

| Cookie | Description |
|---|---|
| %s | Time the system will be shut down |
| %r | Time new connections will be denied |
| %d | Time the current connections will be dropped |
| %C | Current working directory |
| %E | Server administrator's email address as specified in the ftpassess file |
| %F | Available free space in the current working directories partition in kilobytes |
| %L | Local host time |
| %M | Maximum number of allowed connections in this user class |
| %N | Current number of connections for this user class |
| %R | Remote hostname |
| %T | Local time, in the form of Fri Aug 31 21:04:00 2001 |
| %U | Username given at login |

When ftpshut is issued to the system, it creates a file that stores the necessary information. The ftprestart command removes this file for all servers, either canceling the impending shutdown or removing the shutdown file and restarting the FTP server. The ftprestart only has one optional argument, -v, to show version information.

## Use /var/log/xferlog to View a Log of Server Transactions

The xferlog file gives a log of what transactions have occurred with the FTP server. Depending on the settings in the /etc/ftpaccess file, the contents of this file can contain the files sent or received by who with a date stamp. Table 23.5 lists the fields of this file. The same information can also be found in the corresponding man page included in the wu-ftpd package.

## TABLE 23.5 /var/log/xferlog Fields

| Field | Description |
|---|---|
| current-time | Current local time in the form of DDD MMM dd hh:mm:ss YYYY, where DDD is the day of the week, MMM is the month, dd is the day of the month, hh is the hour, mm is the minutes, ss is the seconds, and YYYY is the year. |
| transfer-time | Total time in seconds for the transfer. |
| remote-host | Remote hostname. |
| file-size | Size of the transferred file in bytes. |
| filename | Name of the file. |
| transfer-type | A single character indicating the transfer type. The types are a for ascii transfers. b for binary transfers. |
| `special-action-flag` | One or more character flags indicating any special action taken by the server. The values are `C` for compressed files, `U` for uncompressed files, `T` for TARed files, and `-` for no special action taken. |
| `direction` | Indicates whether the file was sent from or received by the server. |
| `access-mode` | The way in which the user logged in to the server. The values are `a` anonymous guest user; `g` guest user, corresponding to the `guestgroup` command in the `/etc/ftpaccess` file; `r` real user on the local machine. If the access mode was guest, the password is given. |
| `service-name` | The name of the service used, usually FTP. |
| `authentication-method` | Type of authentication used. The values are `0`: none; `1`: RFC931 Authentication (a properly formed email address). |
| `authenticated-user-id` | This is the user ID returned to the server based on the authentication method used to access the server. An `*` is used when an authenticated user ID cannot be found. |
| `completion-status` | A single character field indicating the status of the transfer. The values are `c`: completed transfer; `i`: incomplete transfer. |

An example of this file is seen in Listing 23.5.

## LISTING 23.5 Sample `/var/log/xferlog` File with Inbound and Outbound Logging

```
Mon Sep  3 07:13:05 2001 1 localhost.localdomain 100
    /var/ftp/pub/README  o  o  testing@test.com ftp 0 * c
Mon Sep  3 02:35:35 2001 1 helios 8 /var/ftp/pub/configuration a
    _o  o  testing@test.com ftp 0 * c
Mon Sep  3 02:35:35 2001 1 helios 8 /var/ftp/pub/temp.txt a  o  a
    testing@test.com ftp 0 * c
Mon Sep  3 02:35:35 2001 1 helios 8 /var/ftp/pub/ftp-server-
    0.17-14.i386.rpm  a  o  testing@test.com ftp 0 * c
Mon Sep  3 02:35:35 2001 1 helios 8 /var/ftp/pub/wu-ftpd-2.6.1-
    22.i386.rpm  a  o  a  testing@test.com ftp 0 * c
```
