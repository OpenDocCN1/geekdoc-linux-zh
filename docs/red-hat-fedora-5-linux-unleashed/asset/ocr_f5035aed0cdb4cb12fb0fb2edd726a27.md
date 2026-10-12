# **Use /var/log/xferlog to View a Log of Server Transactions**

The *xferlog* file gives a log of what transactions have occurred with the FTP server. Depending on the settings in the `/etc/ftpaccess` file, the contents of this file can contain the files sent or received, by who, with a date stamp. Table 24.5 lists the fields of this file. The same information can also be found in the corresponding man page included in the *wu-ftp* RPM.

**TABLE 24.5 /var/log/xferlog Fields**

| Field | Description |
|---|---|
| current-time | Current local time in the form of DDD MMM dd hh:mm:ss YYYY, where DDD is the day of the week, MMM is the month, dd is the day of the month, hh is the hour, mm is the minutes, ss is the seconds, and YYYY is the year. |
| transfer-time | Total time in seconds for the transfer. |
| remote-host | Remote hostname. |
| file-size | Size of the transferred file in bytes. |
| filename | Name of the file. |
| transfer-type | A single character indicating the transfer type. The types are a for ASCII transfers b for binary transfers |
| symbol-action-flag | One or more character flags indicating any special action taken by the server. The values are c for compressed files u for uncompressed files t for TARred files - for no special action taken |
| direction | Indicates whether the file was sent from or received by the server. |
| access-mode | The way in which the user logged in to the server. The values are a for an anonymous guest user g for a guest user, corresponding to the guestgrp command in the /etc/ftpaccess file r for a real user on the local machine |
| username | If logged in as a real user, the username. If the access mode was guest, the password is given. |
| service-name | The name of the service used, usually FTP. |
| authentication-method | Type of authentication used. The values are 0 for none 1 for RFC931 authentication (a properly formed email address) |
| authenticated-user-id | This is the user ID returned to the server based on the authentication method used to access the server. An * is used when an authenticated user ID cannot be found. |
| completion-status | A single-character field indicating the status of the transfer. The values are c for a completed transfer i for an incomplete transfer |