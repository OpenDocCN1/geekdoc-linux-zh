# Samba Daemons

The sharing of directories and printers on a Microsoft-style network requires several daemons and a number of related commands. Working together, the commands can help configure Samba, and the daemons help it communicate through the different communication ports described earlier in this chapter.

Samba includes a substantial number of commands that run the service, as well as aid in configuration. The most important of the commands are the binary files in the /usr/sbin directory that start the various Samba services.

You need two daemons to run Samba: the main Samba service (smbd) and the NetBIOS name service (nmbd). In addition, most administrators will want to run the Winbind service (winbindd) for user and host name resolution. All three are configured through the /etc/samba/smb.conf configuration file.

If you want to make sure the services are running the next time Linux is booted, the associated scripts in the /etc/init.d directory are smb, nmb, and winbind. They start the associated smbd, nmbd, and winbindd daemons with the following options in the /etc/sysconfig/samba file:

```
SMBDOPTIONS="-D"
NMBDOPTIONS="-D"
WINBINDOPTIONS=""
```

Yes, while no options are included for the winbind daemon, they can be included in quotes in the noted file. To confirm the way a daemon is running, the ps aux | grep smb command can help. For example, the following output to the ps aux | grep smb command confirms that the Samba service is running with the -D switch:

```
root 12836 0.0 0.2 203612 1648 ? S Mar08 0:00 smbd -D
```

# Samba Server Global Configuration

You can configure a Samba server through the main Samba configuration file, /etc/samba/smb.conf. This file is long and includes a number of commands that require some understanding of the concepts associated with Microsoft Windows networking. Fortunately, the default version of this file also includes helpful documentation with suggestions and useful options.

Unlike with some other services, the default Samba configuration file includes a number of commented directives other than the default. The default value of such directives can be found in the man page for the smb.conf file.