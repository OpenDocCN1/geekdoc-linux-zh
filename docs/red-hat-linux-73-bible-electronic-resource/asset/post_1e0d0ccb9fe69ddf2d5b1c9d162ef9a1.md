
**Guest** level of permission to access and change files. See the sidebar describing guest accounts for further information.

- **server** — The security option that, from the client's point of view, is the same as user security, in that the client still has to provide a valid user name/password combination to use the Samba server at all. The difference is on the server side. With server security, the user name/password is sent to another SMB server for validation. If this fails, Samba will try to validate the client using *user security*.

- **domain** — The security option that, from the client's point of view, looks the same as *user security*. This setting is used only if the Samba server has been added to a Windows NT domain (using the *smbpasswd* command). When a client tries to connect to the Samba server in this mode, its user name and password are sent to a Windows NT Primary or Backup Domain controller. This is accomplished the same way that a Windows NT server would perform validation. Valid Red Hat Linux user accounts must still be set up.

- **Encrypt Passwords** — Controls whether encrypted passwords can be negotiated with the client. This is off (No) by default. For *domain security*, this value must be true. Later versions of Windows NT (4.0 SP3 or later) and Windows 98 and Windows 2000 expect encrypted passwords to be on.

- **Update Encrypted** — Allows users who log in with a plain-text password to automatically have their passwords updated to an encrypted password when they log in. Normally, this option is off. It can be turned on when you want an installation using plain-text passwords to have everyone updated to encrypted password authentication. It saves users the trouble of running the *smbpasswd* command directly from the server. After everyone is updated, this feature can be turned off. When this option is on, the encrypt passwords option should be set to no.

- **Guest Account** — Specifies the user name for the guest account. When a service is specified as Guest OK, the user name entered here will be used to access that service. The account is usually the *nobody* user name.

> **TIP:** Make sure that the guest account is a valid user. (The default of *nobody* should already be set up to work.) Without a valid user as the guest account, the *IPC$* connection that lists the shared resources will fail.

- **Hosts Allow** — Contains a list of one or more hosts that are allowed to use your computer's Samba services. By default, users from any computer can connect to the Samba server (of course, they still have to provide valid user names and passwords). Usually, you use this option to allow connections from specific computers or computer networks that are excluded by the Hosts Deny option.

- **Hosts Deny** — Contains a list of one or more hosts from which users are not allowed to use your computer's Samba services. You can make this option fairly restrictive, and then add the specific hosts and networks you want to use the Samba server. By default, no hosts are denied.

### Assigning Guest Accounts

Samba always assigns the permissions level of a valid user on the Red Hat Linux system to clients who use the server. In the case of share security, the user is assigned a guest account (the "nobody" user account by default).

If the guest account value isn't set, Samba goes through a fairly complex set of rules to determine which user account to use. The result is that it can be hard to assure which user permissions will be assigned in each case. This is why it is recommended to use "user security" if you want to provide more specific user access to your Samba server.

### Logging options

The following options help define how logging is done on your Samba server.

- **Log File** — Defines the location of the Samba smb log file. By default, Samba log files are contained in `/var/log/samba` (with file names `log.nmbd`, `log.smbd`, and `smb.log`). In this option, the `%m` is replaced by `smb` to set the smb log file as `/var/log/samba/smb.log`.

- **Max Log Size** — Sets the maximum amount of space, in kilobytes, that the log files can consume. By default, the value is set to 0 (no limit).

### Tuning options

The Socket Options option lets you pass options to the protocols Samba uses to communicate. The following options are set by default: `TCP_NODELAY`, `SO_RCVBUF=8192`, and `SO_SNDBUF=8192`. The first option disables Nagle's algorithm, which is used to manage the transmission of TCP/IP packets. The other two options set the maximum size of the sockets receive buffer and send buffer to 8192, respectively. These options are set to improve performance (reportedly up to 10 times faster than without setting these options). In general, you shouldn't change these options.

### Printing options

The Printing option is used to define how printer status information is presented. For Linux systems (including Red Hat Linux), the value is typically `LPRNG`. You can use printing styles from other types of operating systems, such as UNIX System V (sysv), AIX (aix), HP UNIX (hpx), and Berkeley UNIX (bsd), to name a few.

### Browse options

A browse list is a list of computers that are available on the network to SMB services. Clients use this list to find computers that are not only on their own LAN, but also computers in their workgroups that may be on other reachable networks.

With the latest release of Samba, browsing is supported. In Samba, browsing is configured by options described below and implemented by the *nmbd* daemon. If you are using Samba for a workgroup within a single LAN, you probably don't need to concern yourself with the browsing options. If, however, you are using Samba to provide services across several physical subnetworks, you may consider configuring Samba as a domain master browser. Here are some points to think about:

- Samba can be configured as a master browser. This allows it to gather lists of computers from local browse masters to form a wide-area server list.
- If Samba is acting as a domain master browser, Samba should use a WINS server to help browse clients resolve the names from this list.
- Samba can be used as a WINS server, although it can also rely on other types of operating systems to provide that service.
- There should be only one domain master browser for each workgroup. Don't use Samba as a domain master for a workgroup with the same name as an NT domain.

If you are working in an environment that has a mix of Samba and Windows NT servers, you should use an NT server as your WINS server. If Samba is your only file server, you should choose a single Samba server (*nmbd* daemon) to supply the WINS services.

> **NOTE:** A WINS server is basically a name server for NetBIOS names. It provides the same service that a DNS server does with TCP/IP domain names: it can translate names into addresses. A WINS server is particularly useful for allowing computers to communicate with SMB across multiple subnetworks where information is not being broadcast across the subnetworks' boundaries.

To configure the browsing feature in Samba, you must have the workgroup named properly (described earlier in this section). Here are the global options related to SMB browsing.

> **NOTE:** If you have trouble getting browsing to work, check the nmbd log file `(/var/log/samba/log.nmb)`. If you need more detail, increase the debug information level to 2 or 3 (described earlier in this section) and restart Samba. The log can tell you if your Samba server is the master browser and, if so, which computers are on its list.

- **OS Level** — Set a value to control whether your Samba server (*nmbd* daemon) may become the local master browser for your workgroup. Raising this setting increases the Samba server's chance to control the browser list for the workgroup in the local broadcast area.

If the value is 0, a Windows machine will probably be selected. A value of 60 will probably ensure that the Samba server is chosen over an NT server. The default value is 20.

- **Preferred Master** — Set this to Yes if you want to force selection of a master browser. By setting this to Yes, the Samba server also has a better chance of being selected. (Setting Domain Master to Yes along with this option should ensure that the Samba server will be selected.) This is set to Auto by default, which causes Samba to try to detect the current master browser before taking that responsibility.

- **Local Master** — Set this to Yes if you want the Samba server to become the local browser master. (This is not a guarantee, but gives it a chance.) Set the value to No if you do not want your Samba server selected as the local master. Local Master is Auto by default.

- **Domain Master** — Set this to Yes if you want the Samba server (nmbd daemon) to identify itself as the domain master browser for its workgroup. This list will then allow client computers assigned to the workgroup to use SMB-shared files and printers from subnetworks that are outside of their own subnetwork. This is set to No by default.

### WINS options

Use the WINS options if you want to have a particular WINS server provide the name-to-address translation of NetBIOS names used by SMB clients. As noted earlier, you probably don't need to use a WINS server if all of the clients and servers in your SMB workgroup are on the same subnetwork. That's because NetBIOS names can be obtained through addresses that are broadcast. It is possible to have your Samba server provide WINS services.

- **WINS Server** — If there is a WINS server on your network that you want to use to resolve the NetBIOS names for your workgroup, you can enter the IP address of that server here. Again, you will probably want to use a WINS server if your workgroup extends outside of the local subnetwork.

- **WINS Support** — Set this value to Yes if you want your Samba server to act as a WINS server. (It's No by default.) Again, this is not needed if all the computers in your workgroup are on the same subnetwork. Only one computer on your network should be assigned as the WINS server.

Besides the values described here, you can access dozens more options by clicking the Advanced View button. When you have filled in all the fields you need, click Commit Changes at the bottom of the screen to have the changes written to the /etc/samba/smb.conf file.

### Configuring shared file systems with SWAT

To make your shared directory available to others, you can add an entry to the SWAT window. To use SWAT to set up Samba to share directories, do the following:
