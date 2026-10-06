# Chapter 18  Setting Up Windows Interoperability with Samba 517

```
# smbpasswd -a vwh
NIS SMB password:
Retype SMB password:
```

Enter the password that you want to assign to the specified user for it—the password is not echoed to the screen as you type. When you have entered the specified user's Samba password, you must type it again to verify that you didn't mistype the password.

The user you are adding to the Samba password file must be a valid Linux user on your system, for whom an entry exists in the standard Linux /etc/passwd file.

If you execute the smbpasswd command with an argument, the command attempts to change the password for the current user. If you specify a username without specifying the -a option, the smbpasswd command attempts to change the Samba password for the specified user.

For complete information about the smbpasswd command, see the online manual for the command, available by typing man smbpasswd in any console, xterm, or other terminal emulation window.

# Working with the Winbind Daemon

The Winbind daemon, winbindd, enables the Linux name service (SSS) to retrieve user and group information from a Windows primary domain controller (PDC). This provides a networked authentication mechanism similar to the Network Information System (NIS) and NIS+ often used in computing environments that make heavy use of Sun's Network File System (NFS). The Winbind daemon enables Windows users to log in on a Linux machine using the Windows credentials provided by the PDC without requiring any local user and group entries in the Linux password file.

To use winbind, you must do:

+   Add Winbind entries to the /etc/nswitch.conf file that tells your Linux system that it uses as a for authentication and in which those services should be queried for valid authentication information. entries should look like the following:
```
passwd: files winbind
group:  files winbind
```

+   Modify the auth (authentication) entries in all of the Pluggable Authentication Module (PAM) configuration files in the directory /etc/pam.d to contain authentication entries such as the following: