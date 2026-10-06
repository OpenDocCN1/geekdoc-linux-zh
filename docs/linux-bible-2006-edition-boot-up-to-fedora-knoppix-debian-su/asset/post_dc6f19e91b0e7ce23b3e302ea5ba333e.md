
# Chapter 27 ✦ Running a File Servers 737

- **Passwd program**—Indicates which password program to use to change Linux user passwords. By default, `/usr/bin/passwd` is used, with the current username (`%u`) inserted.

- **Passwd chat**—Sets the chat that goes between the Samba daemon (smbd) and the Linux password program (`/usr/bin/passwd` by default) when smbd tries to synchronize SMB passwords with Linux user passwords.

- **Username map**—Sets the file used to map Samba usernames. By default, the file is `/etc/samba/smbusers`.

- **UNIX password sync**—With this (Yes), Samba tries to update a user's Linux password with his or her SMB password when the SMB password is changed. To do this, smbd runs the `passwd` command as the root user. It is by default.

- **Guest account**—Specifies the name for the guest account. When a service is specified as Guest OK, the name entered here is used to access that service. The account is the `nobody` username.

> Make that the guest account is a valid user. (The default of `nobody` should already be up to you.) With an invalid user as the guest account, the `IPC$` connection to the shared resources fails.

- **Hosts allow**—Contains a list of one or more hosts that are allowed to use your computer's Samba services. By default, users from any computer can connect to the Samba server (of course, they still provide valid usernames and passwords). Generally, you use this option to allow connections from specific computers (such as 10.0.0.1) or computer networks (such as 10.0.0.) that are excluded by the hosts deny option.

- **Hosts deny**—Contains a list of one or more hosts which users are not allowed to use your computer's Samba services. You can make this option fairly restrictive, and then add the specific hosts and networks you want to use the Samba server. By default, hosts are denied.

# Logging Options

The following options define how logging is done on your Samba server:

- **Log level**—Sets the debug level used when logging Samba activity. Raise the level from the default (0) to log more Samba activity.

- **Log file**—Defines the location of the Samba smbd log file. By default, Samba log files are contained in `/var/log/samba` (with names `log.nmbd`, `log.smbd`, and `smbd.log`). In this option, the `%m` is replaced by smbd to set the log file at `/var/log/samba/smbd.log`.

- **Max size**—Sets the maximum amount of space, in kilobytes, that the log files can consume. By default, the value is set to 0 (no limit).

![](img/a2d958d7eab32ca5b89b2b8af808aa70_768_0.png)

# Assigning Guest Accounts

Samba always assigns the permissions level of a valid user on the Linux system to clients who use the server. In the case of share security, the user is assigned a guest account (the nobody account by default).

If the guest account value isn't set, Samba goes through a fairly complex set of rules to determine which user account to use. The result is that it hard to ensure which user permissions will be assigned in each account. That's why user security is recommended if you want to provide more specific user access to your Samba server.

### Performance Options

### Socket Options option

The Socket Options option lets you pass options to the protocols Samba uses to communicate. The following options are set by default: TCP_NODELAY, SO_RCBUF=8192, and SO_SNDBUF=8192. The first option disables Nagle's algorithm, which is used to manage the transmission of TCP/IP packets. The other two set the maximum size of the socket receive and send buffer to 8192, respectively. These options are set to improve performance (reportedly up to ten times without setting these options). In general, you shouldn't change these options.

### Printing Options

The printing options are used to define how printer status is presented. For the overwhelming majority of Linux systems, the printing value is set to cups. You can use printing styles from other types of operating systems, such as UNIX V (sys), ARX (aix), HP (unix), and Berkeley (bsd), to name a few. LP (lp), offered by many UNIX systems, is also included. Other printing options enable you to redefine the location of basic commands (lpq, lpr, and so on) and printing files (such as printcap).

### Browse Options

A browse is a list of computers that are available on the network. Clients use this list to find computers on their own LAN and also workgroups that may be reachable through networks. In Samba, browsing is configured by options described later and implemented by the nmbd daemon. If you are using Samba for workgroup within a single LAN, you probably don't need to concern yourself with the browsing options. However, if you are using Samba to provide services across several subnets, you might want to consider configuring Samba as domain master. Here are some points to think:

- Samba can be configured as domain master, which allows it to gather lists of computers from local to form a wide-area list. (Browse masters keep track of available shared directories and printers as necessary.)

- If Samba is acting as domain master, Samba should use WINS server to help resolve names.

- Samba can be used as WINS server, although it can also rely on other types of operating systems to provide that service.

- There should be only one domain master for each subgroup. Don't use Samba as domain master for a subgroup with the same name as NT.

- WINS is basically a name server for NetBIOS names. It provides the service that a DNS server does with TCP/IP names. WINS is particularly useful for allowing computers to communicate across multiple subnetworks where information is not broadcast across boundaries. To configure the browsing feature in Samba, you must have the group named properly (described earlier). Here are the global options related to broadcasting:

- OS level—Set a value to control whether your Samba server (nmbd daemon) may become the local master for your subgroup. This increases the Samba server's chance to control the browse list for local area broadcast. If the value is 0, Windows machine will probably be selected. A value of 1 ensures that the Samba server is chosen over NT server. The default is 2.

- Preferred master—Set this to Yes if you want to force selection of Samba server and give it a better chance of being selected. (Setting Domain Master Yes with this option ensures that Samba server will be selected.) This is set to Auto, which causes Samba to try to detect the current master before taking responsibility.

- Local master—Set this to Yes if you want the Samba server to become the local master. (This is not a guarantee, but gives it a chance.) Set the value to No if you do not want your Samba server selected as local master. Local master is Auto by default.

- Domain master—Set this to Yes if you want the Samba server (nmbd daemon) to identify itself as the domain master for your workgroup. This list will allow client computers assigned to the workgroup to use SMB-shared files and printers from subnetworks that are outside your own subnet. This is set to No by default.

If browsing is not working, check the nmbd log file (`/var/log/samba/log.nmbd`). To get more detail, increase the debug level to 2 or 3 (described earlier in this section) and restart Samba. The log can tell you if your Samba server is the master browser and, if so, computers on its list.

# WINS Options

Use the WINS options if you want to have a particular WINS server provide the name-to-address translation of NetBIOS names used by SMB clients:

- server—If there is a WINS server on your network that you want to resolve the NetBIOS names for your workgroup, enter that server's IP address here. Again, you probably use a WINS server if your workgroup extends outside the local subnet.

- support—Set this value to Yes if you want your Samba server to act as a WINS server. (It's No by default.) Again, it is not needed if all the computers in your workgroup are on the same subnet. Only one computer on your network should be assigned as the WINS server.

In addition to the values described here, you can access dozens more options by clicking the Advanced View. When you have filled in all the fields you need, click Commit Changes on the screen to have the changes written to the `/etc/samba/smb.conf` file.

# Configuring Shared Directories with SWAT

To make your shared directory available to others, add an entry to the SWAT directory. To use SWAT to set up Samba share directories, do the following:

You may see one or more security warnings during the course of this procedure. These messages warn you that someone could potentially view the data you are sending to SWAT. If you are working on your local host or on a private LAN, the risk is minimal.

1. From the main SWAT window, click the SHARES button.
2. Type the name of the directory you want to share in the Create Share box, and then click Create Share.
3. Add any of these options:
- Comment — A few words to describe the shared directory (optional).
- Path — The path name of the directory you are sharing.
