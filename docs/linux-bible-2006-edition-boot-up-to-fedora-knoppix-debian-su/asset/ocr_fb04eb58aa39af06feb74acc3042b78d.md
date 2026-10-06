# Chapter 27 ✦ Running a File Servers 737

+   **Passwd program**—Indicates which password program to use to change Linux user passwords. By default, `/usr/bin/passwd` is used, with the current username (`%u`) inserted.

+   **Passwd chat**—Sets the chat that goes between the Samba daemon (smbd) and the Linux password program (`/usr/bin/passwd` by default) when smbd tries to synchronize SMB passwords with Linux user passwords.

+   **Username map**—Sets the file used to map Samba usernames. By default, the file is `/etc/samba/smbusers`.

+   **UNIX password sync**—With this (Yes), Samba tries to update a user's Linux password with his or her SMB password when the SMB password is changed. To do this, smbd runs the `passwd` command as the root user. It is by default.

+   **Guest account**—Specifies the name for the guest account. When a service is specified as Guest OK, the name entered here is used to access that service. The account is the `nobody` username.

> Make that the guest account is a valid user. (The default of `nobody` should already be up to you.) With an invalid user as the guest account, the `IPC$` connection to the shared resources fails.

+   **Hosts allow**—Contains a list of one or more hosts that are allowed to use your computer's Samba services. By default, users from any computer can connect to the Samba server (of course, they still provide valid usernames and passwords). Generally, you use this option to allow connections from specific computers (such as 10.0.0.1) or computer networks (such as 10.0.0.) that are excluded by the hosts deny option.

+   **Hosts deny**—Contains a list of one or more hosts which users are not allowed to use your computer's Samba services. You can make this option fairly restrictive, and then add the specific hosts and networks you want to use the Samba server. By default, hosts are denied.

# Logging Options

The following options define how logging is done on your Samba server:

+   **Log level**—Sets the debug level used when logging Samba activity. Raise the level from the default (0) to log more Samba activity.

+   **Log file**—Defines the location of the Samba smbd log file. By default, Samba log files are contained in `/var/log/samba` (with names `log.nmbd`, `log.smbd`, and `smbd.log`). In this option, the `%m` is replaced by smbd to set the log file at `/var/log/samba/smbd.log`.

+   **Max size**—Sets the maximum amount of space, in kilobytes, that the log files can consume. By default, the value is set to 0 (no limit).

![](bbox=[0.135, 0.415, 0.185, 0.465])