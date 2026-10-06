# Chapter 27 ♦ Running a File Servers 735

# Base Options

The following options relate to basic information associated with your Samba server:

+   * **Workgroup** — The name of the group associated with the group of SMB hosts. By default, the value for this field is `WORKGROUP`.

+   * **Realm** — If you are using kerberos authentication, this value indicates the kerberos realm to use. Typically, it is reflected by the host name of the server providing the service.

+   * **NetBIOS name** — The name assigned to this Samba server. You can use the same name as your DNS host name or leave blank, in case the DNS host name is automatically filled for you by default.

+   * **NetBIOS alias** — Enables you to use a way of referring to a host computer (an alias) from the host's TCP/IP DNS name.

+   * **Server string** — A string of identifying the server. This name appears in places such as the printer comment box. By default, it says Samba and the version number.

+   * **Interfaces** — Enables you to use more than one network interface and let Samba several different subnetworks. The form of this field can be `IP Address/Subnetwork Mask`. Or, if you identify a network interface (such as eth0 for the first Ethernet card on your computer). For example, a Class network address may appear as:
`192.168.24.11/255.255.255.0`

# Security Options

Of the security options settings, the first (security) is the most important to get right. It defines the type of security used to give access to the shared files and printers to the client computers (To see some of the fields described here, you need to click the Advanced view)

+   * **Security** — Sets how password and user information is transferred to the Samba server from the client computer. As noted earlier, it's important to get this value right. Samba 2.0 and later has a different default value for security (`security-user`) than the earlier versions of Samba do (`security-share`). If you are coming from an earlier version of Samba and clients are failing to access your server, this is a good place to start. Here are your options:

+   * **user** — The most common type of security used to share files and printers to Windows 95/2000/NT/XP clients. It is the default set with Samba in the current release. This setting is appropriate if users are doing a lot of file sharing (as opposed to a Samba server mostly as a print server). It requires that a user provide a username/password before using the server. The easiest way to get this method working is to give a Linux