
The `log.nmb` and `log.smb` files report status and error conditions for the `nmbd` and `smbd` servers, respectively. Additionally, whenever any errors are reported for any connecting client host (such as authentication failures), these messages are printed into a `log.<name>` file for that client. Note that this can result in a lot of files cluttering up your `/var/log` directory. You can switch to a combined log format by commenting out the `log file` line in `smb.conf`:

```
# this tells Samba to use a separate log file for each machine
# that connects
;	log file = /var/log/log.%m
```

SMB errors for individual hosts will go into `log.smb` with this line commented out.

Another useful line to modify is the `max log size` line, which is set to `50KB` by default. This control allows you to set the “rollover” size for any of the log files. When any Samba log file reaches the size you've designated, the file's renamed by appending `.old` to the filename, and new log entries are added to a new file. The `.old` file is overwritten at the next rollover.

```
# Put a capping on the size of the log files (in Kb).
	max log size = 50
```

### Samba Variables

Configuration parameters in `smb.conf` don't have to be hard-wired. You have a number of variable substitutions at your disposal, so you can set certain options to be dynamically determined, depending on the conditions of the connection. For example, you can set an option to reflect the client's username with the `%u` variable, allowing you to set a parameter such as `path = /usr/local/share/user-files/%u`. The user `harris` would thus receive the path `/usr/local/share/user-files/harris`.

Here are a few of the most useful variables:

- `%u`—The client's username.
- `%g`—The primary group name of `%u`.
- `%S`—The name of the current service, if any.
- `%H`—The home directory of the user given by `%u`.
- `%h`—The Internet hostname of the Samba server.
- `%M`—The Internet hostname of the client machine.
- `%L`—The NetBIOS name of the Samba server. This allows you to change your config based on what the client calls you; your server can have a “dual personality.”
- `%m`—The NetBIOS name of the client machine.
- `%I`—The IP address of the client machine.
- `%T`—The current date and time.
- `$$`(`envvar`)—The value of the environment variable `envvar`.

The complete list of variable substitutions is available in `man smb.conf`.

## Other Samba Components

The Samba package includes a number of additional tools:

- `smbclient`—A simple FTP-like client that allows you to connect to remote SMB shares and print to remote Windows printers.
- `testparm`—A configuration file syntax checker that tests your `smb.conf` for correctness; similar to `apachectl configtest` for Apache.
- `testprns`—Tests whether the printers specified in `/etc/printcap` will work properly with Samba.
- `smbstatus`—Displays current connections to the Samba server. SWAT, as you saw earlier, has a page that shows the formatted output of this command in a Web browser.
- `nmblookup`—Allows you to make NetBIOS name queries like those made by Windows hosts connecting directly to SMB shares by name.
- `make_smbcodepage`—A tool that allows you to create new SMB code page definitions for Samba.

These tools also are described in `man samba`; each one has its own man page for further details. Finally, these tools are in addition to the `smbd`, `nmbd`, and `smbpasswd` utilities discussed previously in this chapter. Each of those has its own man page as well.

## Future Samba Development

At the time of this writing, the most recent version of Samba in the ports is 2.2.6. This version incorporates many recent enhancements to Windows networking, enabling features that are new in Windows 2000 and XP and increasing the level of interoperability between Windows and Unix file servers. Some of the new features are as follows:

- Automatic downloading of Windows NT/2000 printer drivers from the Samba server, if they are not present on the client machine
- Unification of Windows NT/2000 and Unix Access Control Lists (ACLs) and remote manageability of such lists from Windows machines
- Built-in Windows NT/2000 login authentication
- Microsoft Distributed File System (DFS) support and the capability to act as a DFS server for Windows clients

See the documentation at http://www.samba.org for further details on these and other new features.

## Accessing Shared Files on a Windows System (the smbfs Filesystem)

SMB file sharing can work both ways. Samba allows you to set up your FreeBSD machine as an SMB server only, but there is a way to set it up as a client and mount a remote SMB share like any other filesystem. This involves `smbfs`, available as a standard kernel module as of FreeBSD 4.4, and in the ports (`/usr/ports/net/smbfs`) in earlier versions.

The `smbfs` implementation in FreeBSD includes an `smbfs.ko` kernel module in `/modules` and a `mount_smbfs` tool in `/sbin` that works like all the other `mount_*` tools you saw in Chapter 8, “The FreeBSD Filesystem.” The best documentation for `smbfs` is found in the `man mount_smbfs` page.

To mount an SMB filesystem using `smbfs`, use `mount_smbfs` with a few basic options. The `-I` flag specifies the hostname or IP address, and the two remaining arguments are the remote share name (of the form `//<user>@<NetBIOS_name>/<share_name>`) and the local mount point. To mount the share called `public` from a Windows machine called `gaming-pc` onto the local `/smb/public` directory, use the following syntax:

```text
# mount_smbfs -I 64.41.131.139 //guest@gaming-pc/public /smb/public
```

You will be prompted for a password. Use a blank password if the share is set to allow full access; use the appropriate password if the share is set to read-only or password-protected mode.

> **NOTE**
>
> The `smbfs.ko` kernel module is loaded automatically when needed by `mount_smbfs`. If you want to, you can load it at boot time by adding the following line to `/boot/loader.conf`:
>
> ```text
> smbfs_load="YES"
> ```
>
> However, this is probably not necessary.

To add an SMB share to `/etc/fstab`, use the following syntax:

```text
//guest@gaming-pc/public /smb/public smbfs rw,noauto 0 0
```

The mount-a process that occurs during startup will mount this share automatically when the FreeBSD system boots.

## CHAPTER 34

## Dynamic Host Configuration Protocol (DHCP)

DHCP, which stands for *Dynamic Host Configuration Protocol*, is a network protocol that allows a client to obtain its IP address, name server information, gateway server information, and several other network-configuration options from a server that is running a DHCP server.

This chapter will show you how to configure a DHCP client on your FreeBSD system (so that it can obtain an IP address from a DHCP server). It will also show you how to configure a DHCP server.

### How DHCP Works

A detailed discussion of how DHCP works is beyond the scope of this book, but here is a basic rundown of what happens.

In FreeBSD, a client program called `dhclient` allows FreeBSD to act as a DHCP client. When a system configured to use DHCP boots and `dhclient` starts, it will send out broadcast requests on port 68. These requests are sent in UDP format.

If there is a DHCP server on the network, it will be listening to port 68 for these requests. When it receives a request for configuration information, it will check its database for a free IP address that can be assigned to the client. It will then send back all the configuration information that the client requests on port 67, once again using UDP. The IP address that is assigned to the client will be removed from the pool of available addresses so that it is not assigned to another client that requests DHCP configuration information.

### IN THIS CHAPTER

- How DHCP Works
- Advantages of DHCP over Static IP Addresses
- Kernel Configuration for DHCP
- Enabling DHCP
- The `dhclient` Program
- DHCP Server Daemon
- Configuring the `dhcpd` Configuration File
