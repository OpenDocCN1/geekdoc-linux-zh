
> **Tip**
>
> For simple administration tasks with the Samba server, there is also the program swat. It provides a simple web interface with which you can conveniently configure the Samba server. In a web browser, call up `http://localhost:901` and log in as user root. swat is also activated in the files `/etc/inetd.conf` and `/etc/services`. More information about swat can be found in its man page.

## Samba as Login Server

In networks where predominantly Windows clients are found, it is often preferable that users may only register with a valid account and password. This can be brought about with the help of a Samba server. In a pure Windows network, a Windows NT server takes on this task. This is configured as a Primary Domain Controller (PDC). The following entries must be made in the [global] section of the smb.conf.

```text
[global]
workgroup = TUI-NET
domain logons = yes
domain master = yes
```

*File 61:*

If encrypted passwords are used for verification purposes, the Samba server must be able to handle these. The entry encrypt passwords = yes in the [global] section enables this functionality. In addition, it is necessary to prepare user accounts and passwords in an encryption format that conforms with Windows. This is done with the command smbpasswd -a name. Since, in accordance with the Windows NT domain concept, the computers themselves need a domain account, this is created with the following commands:

```text
useradd -m machinename
smbpasswd -a -m machinename
```

*File 62: Adding a Machine Account*

With the useradd command, a masked dollar sign, masked by a backslash, is added. The command smbpasswd includes this automatically when the -m parameter is used.

## Installation of Clients

First, it should be mentioned that clients can only access the Samba server via TCP/IP. NetBEUI and NetBIOS via IPX are not available at the moment. Since TCP/IP is becoming more and more popular, even with Novell and Microsoft, it is not certain whether this is going to change in the near future.

### Windows 95/98

Windows 95/98 already has built-in support for TCP/IP. As with Windows for Workgroups, however, this is not installed as the default. To add TCP/IP, go to ‘Control Panel’ → ‘System’ and choose ‘Add’ → ‘Protocols’ → ‘TCP/IP from Microsoft’. Be sure to enter your network address and network mask correctly. After rebooting your Windows machine, you will find the properly configured Samba server in networks (double-click on the network icon on your desktop).

> **Tip**
>
> To use a printer on the Samba server, install the standard or Apple-PostScript printer driver from the corresponding Windows version. It is best to link this to the Linux printer queue, which includes an automatic apsfilter recognition.

## Optimization

It should first be pointed out here that Samba, in its default version, is prepared for handling Windows NT server. It is, therefore, actually not necessary to carry out optimizations, because the many tuning options only result in a minimal difference in terms of speed. The standard configuration in `/etc/samba/smb.conf` is, of course, not tuned to every network and the way the network is used, so that this can also be optimized. Since this fine-tuning is dependent on many factors, no universal solution can be provided. Look at the help files and the many tips on optimization in the files `/usr/share/doc/packages/samba/textdocs/Speed.txt` and `/usr/share/doc/packages/samba/textdocs/Speed2.txt`.

## Netatalk

With the package `netatalk`, obtain a high-performance file and print server for MacOS clients. With it, access data on a Linux machine from a Macintosh or print to a connected printer.

Netatalk is a suite of Unix programs that run on kernel-based DDP (Datagram Delivery Protocol) and implement the AppleTalk protocol family (ADSP, ATP, ASP, RTMP, NBP, ZIP, AEP, and PAP). AppleTalk is, in effect, an equivalent to the more familiar protocol known as TCP (Transmission Control Protocol). It has counterparts to many services available on TCP/IP, including services for resolving host names and time synchronization. For example, the command `nbplkup` (NBP, Name Binding Protocol) is used instead of `nslookup` (DNS, Domain Name Service) and `aecho` (AEP, AppleTalk Echo Protocol) instead of `ping` (ICMP ECHO_REQUEST, Internet Control Message Protocol).

The three daemons described below are normally started on the server:

- `atalkd` (“AppleTalk Network Manager”) that somewhat correlates the programs `ifconfig` and `routed`
- `afpd` (AppleTalk Filing Protocol daemon), which provides an interface for Macintosh clients to Unix file systems
- `papd` (Printer Access Protocol daemon), which makes printers available in the (AppleTalk) network.

Of course, you can export server directories not only via Netatalk, but also, at the same time, via Samba for Windows clients (see Section Clients on page 374) and via NFS (see *NFS — Shared File Systems* on page 365), which is very useful in heterogeneous network environments. This centralizes the management of data backup and user permissions on the Linux server.

Note:

- Due to Macintosh client restrictions, the user passwords on the server cannot be longer than eight characters.
- Macintosh clients cannot access Unix files with names longer than 31 characters.
- File names may not contain colons (`:`) because they serve as path name separators in MacOS.

The package `netatalk`, series 2 has to be installed.

## Configuring the File Server

In the default configuration, Netatalk is already fully functional as a file server for home directories of the Linux system. To use the extended features, define some settings in the configuration files. These are located in the `/etc/atalk` directory.

All configuration files are text files. Text that follows a hash mark `#` (comments) and empty lines can be disregarded.

### Configuring the Network — atalkd.conf

Define, in `/etc/atalk/atalkd.conf`, over which interfaces services are provided. This is usually eth0, which means that it suffices if the only value entered here is eth0. In the example file that comes with Netatalk, this is the case. Enter additional interfaces to use several network cards at the same time. When the server is started, it will search the network for already existing zones and servers and modify the corresponding lines by entering the set AppleTalk network addresses. You will then find a line such as

```
eth0 -phase 2 -net 0-65534 -addr 65280.57
```

at the end of the file. To make more complex configurations, find examples for this in the configuration file. Find documentation on additional options in the manual page of afpd.

### Defining File Servers — afpd.conf

The `afpd.conf` file contains definitions for how your file server appears on MacOS machines as an item under the ‘Chooser’ dialog. As is the case with the other configuration files, these also contain detailed comments explaining the wide variety of options.

If you do not change anything here, the default server will simply be started and displayed with the host name in the ‘Chooser’. Therefore, you do not necessarily have to enter anything. However, you can give additional file servers a variety of names and options here. For instance, to provide a specific “guest server” where everybody can save files as “guest”,

```
"Guest server" -uamlist uams_guest.so
```

Define a server that denies guests access, but which is only accessible for users who already exist in the Linux system with

```
"Font server" -uamlist uams_clrtxt.so,uams_dhx.so
```

This behavior is controlled by the option `uamlist`, followed by a list of authentication modules to use, separated by commas. If you do not provide this option, all procedures are active by default.

An AppleShare server not only provides its services by default via AppleTalk, but also (“encapsulated”) via TCP/IP. The default port is 548. Assign dedicated ports to additional AppleShare servers (on the same machine) if these are to likewise run via TCP. The availability of the service via TCP/IP enables access to the server even over non-AppleTalk networks, such as the Internet.

In this case, the syntax would read:

```
"Font server" -uamlist uams_clrtxt.so,uams_dhx.so -port 12000
```

The AppleShare server, set to the port 12000, then appears in the network with the name “Font server” and will not allow guest access. In this way, it is also accessible via TCP/IP routers.

The file `AppleVolumes.default` (described in detail below) defines which directories located on the server are made available by each AppleShare server as network “volumes”. Define other files containing unique descriptions for each AppleShare server using the option `-defaultvol`, such as with (in one line):

```
"Guest server" -uamlist uams_guest.so -defaultvol
/etc/atalk/AppleVolumes.guest
```

Further options are explained in the `afpd.conf` file itself.

### Directories and Access Permissions — AppleVolumes.default

Here, define directories to export. The access permissions are defined via the customary Unix user and group permissions. This is configured in the `AppleVolumes.default` file.

> **Note**
>
> Here, the syntax has partially changed. Take this into consideration if you are updating this version from a previous one. For example, it is now
> `allow:` instead of `access=` (a typical symptom would be if, instead
> of the drive descriptions, you were to see a display of the drive options
> on the Mac clients in the ‘Chooser’.) Since the new files are created with
> the `.rpmnew` endings during an update, it is possible that your previous
> settings may no longer function as a result of the modified syntax. We
> recommend creating backups of your configuration files, copying your old
> configurations from them into your new files, then renaming these files to
> the proper names. This way, you will benefit from the current comments
> contained in the configuration files, which provide a detailed explanation
> of the diverse options.
