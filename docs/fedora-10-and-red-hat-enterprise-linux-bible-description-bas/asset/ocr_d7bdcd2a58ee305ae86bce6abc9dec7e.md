# Part IV: Fedora RHEL Network and Server Setup

+   - **netbios name** — The name assigned to this Samba server. You can use the same name as your DNS hostname or leave blank, in which case the DNS hostname is used automatically.

+   - **netbios alias** — Enables you to set a way of referring to a host computer (an alias) that is different from the host's TCP/IP DNS name.

+   - **server string** — A string of text identifying the server. This name appears in places such as the printer comment box. By default, it says Samba and the version number.

+   - **interfaces** — Lets up more than one network interface. This enables Samba to browse several different subnetworks. The first of this can be IP Address/Subnet Mask. Or, you could identify a network interface (such as eth0 for the first Ethernet card on your computer). For example, a Class C network address may appear as `192.168.24.11/255.255.255.0`.

# Security options

Of the security options, the first option (**security**) is the most important to get right. It defines the type of security used to access the shared file systems and printers to the clients. (To see some of the fields described here, you need to click the Advanced view.)

+   - **security** — Sets how password and user information is transferred to the Samba server from the client. As noted earlier, it's important to get this right. The default value for security (`security-user`) is different than the default value for security (`security-share`) in pre-2.0 versions of Samba. If you are coming from an older version of Samba and are clients to access your server, this setting is a good place to start. Here are your common options:

+   - **user** — The most common type of security used to share files and printers to Windows 95/98/2000 and Windows NT clients. It is the default with Samba in the current release. This setting is appropriate if users are doing a lot of file sharing (as opposed to a Samba server used mostly as a print server). It requires that a user provide a user name/password before using the server.

The easiest way to do this is to get a Linux user client user who will use the Fedora or RHEL Samba server. This provides basically the same file permissions to a user account through Samba as the same user would get if he or she logged directly to Linux.

+   - **share** — The share value for security works best for print sharing or for providing file access that is more public (guest sharing). A client doesn't need to provide a valid user name and password to access the server. However, the user will typically have a “guest” level of permission to access and change files. See the sidebar describing guest accounts for further information.

+   - **server** — The security option that, from the client's point of view, is the same as user security, in that the client shall provide a valid user name/password