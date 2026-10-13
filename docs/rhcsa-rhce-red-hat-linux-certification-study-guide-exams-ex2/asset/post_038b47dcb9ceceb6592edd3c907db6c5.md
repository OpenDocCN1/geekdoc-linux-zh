
Red Hat Firewall Configuration tool, it adds the following rules to the /etc/sysconfig/iptables configuration file:

```
-A INPUT -m state --state NEW -m udp -p udp --dport 137 -j ACCEPT
-A INPUT -m state --state NEW -m udp -p udp --dport 138 -j ACCEPT
-A INPUT -m state --state NEW -m tcp -p tcp --dport 139 -j ACCEPT
-A INPUT -m state --state NEW -m tcp -p tcp --dport 445 -j ACCEPT
```

In other words, several services are involved, as described in Table 15-2. You'll note that three of the services use the User Datagram Protocol (UDP), a connectionless protocol. Collectively, the three associated ports specify NetBIOS communication over TCP/IP (NBT).

For Samba client systems, only ports 137 and 138 need to be opened.

## Configure SELinux Booleans for Samba

There are several directives associated with making a Samba server work with SELinux in targeted mode, as described in Table 15-3. Only one of these booleans (samba_export_all_cifs) is enabled by default. However, you may have to activate a number of these booleans to support different Samba functions.

For some readers, this may be getting repetitive. However, SELinux is not well understood even by many Linux experts. So for example, if you want to allow Samba to share local home directories with others on the network, run the following command:

```
# setsebool -P samba_enable_home_dirs 1
```

The -P makes sure the change survives a reboot.

There are cases where it's appropriate to enable the samba_export_all_ro or samba_export_all_rw booleans, such as on directories that are shared through other servers. For example, files that are shared via an Apache web server must be labeled with the httpd_sys_content_t file type.

### TABLE 15-2
Samba Communication Services

| Port/Protocol | Description |
|---|---|
| 137/UDP | NetBIOS name service |
| 138/UDP | NetBIOS datagram service |
| 139/TCP | NetBIOS session service |
| 445/TCP | Microsoft directory services, also known as Samba over IP |

### TABLE 15-3
Samba SELinux Booleans

| Boolean | Description |
|---|---|
| allow_smb_anon_write | Supports the writing of files to directories configured with the public_content_rw_t SELinux setting. |
| cdrecord_read_content | Allows the cdrecord command to read shared Samba (and other network) directories. |
| qemu_use_cifs | Works with access to CIFS filesystems; enabled by default. |
| samba_create_home_dirs | Supports the creation of home directories, normally set up for external users. |
| samba_domain_controller | Allows Samba to act as a domain controller for authentication management. |
| samba_enable_home_dirs | Enables the sharing of home directories. |
| samba_export_all_ro | Sets up read-only access to any directory, even those without the samba_share_t file type label. |
| samba_export_all_rw | Sets up read/write access to any directory, even those without the samba_share_t file type label. |
| samba_run_unconfined | Supports the execution of unconfined scripts from the /var/lib/samba/scripts directory. |
| samba_share_fusefs | Allows Samba to share filesystems mounted to fusefs, a common mount for the Microsoft NTFS filesystem. |
| samba_share_nfs | Enables sharing of NFS filesystems. |
| use_samba_home_dirs | Supports the use of a remote server for Samba home directories. |
| virt_use_samba | Allows a VM to access files mounted to the CIFS filesystem. |

## Configure SELinux File Types for Samba

Normally, Samba can only share those files and directories labeled with the samba_share_t file type. It is true, the samba_share_t file type is not required if the samba_export_all_ro or samba_export_all_rw booleans are enabled. However, that would be a security risk.

So in most cases, you'll want to enable directories (and files therein) with the noted file type with a command like the following:

```
# chcon -R -t samba_share_t /share
```

In addition, to make sure the changes survive a relabel of SELinux, you'll want to set up the file_contexts.local file in /etc/selinux/targeted/contexts/files directory with a command such as the following:

```
# semanage fcontext -a -t samba_share_t /share
```

## Samba Daemons

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

## Samba Server Global Configuration

You can configure a Samba server through the main Samba configuration file, /etc/samba/smb.conf. This file is long and includes a number of commands that require some understanding of the concepts associated with Microsoft Windows networking. Fortunately, the default version of this file also includes helpful documentation with suggestions and useful options.

Unlike with some other services, the default Samba configuration file includes a number of commented directives other than the default. The default value of such directives can be found in the man page for the smb.conf file.

You can edit this file directly or create directory shares using SWAT. Before using any GUI tool, be brave. Study the original /etc/samba/smb.conf file. Once you see how the file is structured, back it up. Try editing the file directly. Try changing the file with the SWAT tool, described later in this chapter. Test the result by restarting the Samba server with the following command:

```
# service smb restart
```

To help you with this process, I'll analyze the default RHEL 6 version of this file. The code shown next is essentially a complete view of this file. In some cases, I've replaced the comments in the file with my own explanations. You might want to browse your own /etc/samba/smb.conf file as well.

The smb.conf file includes two types of comment lines. The hash symbol (#) is used for a general text comment. This is typically verbiage that describes a feature. The second comment symbol is the semicolon (;), used to comment out Samba directives (which you may later wish to uncomment to enable the disabled feature). (Note that the physical dimensions of this book limit the lengths of lines of code. In a few cases, I've modified the code lines slightly to meet this limitation, without changing the intent of any command in this configuration file.)

```
# This is the main Samba configuration file. You should read the
# smb.conf(5) manual page in order to understand the options listed
# here. Samba has a huge number of configurable options (perhaps
# too many!) most of which are not shown in this example.
#
# NOTE: Whenever you modify this file you should run the command
# "testparm" to check that you have not made any basic syntactic
# errors.
```

> exam watch As stated in the Red Hat Exam Prep guide, RHCEs must be able to configure various services, including Samba, for basic operation. Some of the details of the default version of the main Samba configuration go beyond basic operation.

While you need to know what can be done with different global settings, you should change as little as possible. The less you change, the less can go wrong. Perfect configuration files are not required. Configuration files that meet the specific requirements of an exam or a job are.
