
# Turning on SWAT

Before you can use SWAT, you must do some configuration. To set up SWAT to run from your browser, follow these steps:

1.  To turn on the swat service, type the following, as root user, from a Terminal window:
    ```
    # chkconfig swat on
    ```
2.  To pick up the change to the swat service, restart the xinetd start-up script as follows:
    ```
    # service xinetd restart
    ```

When you have finished this procedure, use the SWAT program, described in the next section, to configure Samba.

# Starting with SWAT

You can run the SWAT program by typing the following URL in your local browser:

```
http://localhost:901/
```

At this point, the browser will prompt you for a user name and password. Enter the root user name and password. The SWAT window should appear, as shown in Figure 18-5.

![](img/b22364e57409c2481ba806e4e6b9309c_738_0.png)

Figure 18-5: Use SWAT from your browser to manage your Samba configuration.

> **TIP:** Instead of running SWAT from your local browser, you can run it from another computer on the network by substituting the server computer's name for **localhost**. (To allow computers besides localhost to access the swat service, you must change or remove the only_from = 127.0.0.1 line from the /etc/xinetd.d/swat file and restart the xinetd service.)

The rest of this section describes how to use SWAT to create your configuration entries (in `/etc/samba/smb.conf`) and to work with that configuration.

> **CAUTION:** Any time you use a GUI to change a plain-text configuration file (as you do with SWAT), you may lose some of the information that you put in by hand. In this case, SWAT deletes comment lines and rearranges other entries. To protect changes you have made manually, make a backup copy of your `/etc/samba/smb.conf` file before you edit it with SWAT.

## Creating global Samba settings in SWAT

A group of global settings affects how file and print sharing are generally accomplished on a Samba server. They appear under the [global] heading in the `/etc/samba/smb.conf` file. To edit global variables, click the **GLOBALS** button on the SWAT window.

Seven option types are available: base options, security options, logging options, tuning, printing options, browse options, and WINS options. To view and modify your global Samba server settings, click the **GLOBALS** button. Then add the following options.

> **NOTE:** Each option shown relates to the exact parameters used in the `/etc/samba/smb.conf` file. You can refer to the `smb.conf` man page (type `man smb.conf`) to get more information on these parameters.

### Base options

The following options relate to basic information associated with your Samba server:

- **workgroup** — The name of the workgroup associated with the group of SMB hosts. By default in Fedora, the value for this field is MYGROUP.
- **realm** — If you are using kerberos authentication, this value indicates the kerberos realm to use. Typically, that is reflected by the host name of the server providing the service.
- **netbios name** — The name assigned to this Samba server. You can use the same name as your DNS host name or leave it blank, in which case the DNS host name is used automatically.
- **netbios alias** — This enables you to set a way of referring to a host computer (an alias) that is different from the host’s TCP/IP DNS name.
- **server string** — A string of text identifying the server. This name appears in places such as the printer comment box. By default, it says Samba and the version number.
- **interfaces** — Lets you set up more than one network interface. This enables Samba to browse several different subnetworks. The form of this field can be `IP_Address/Subnetwork_Mask`. Or, you could identify a network interface (such as eth0 for the first Ethernet card on your computer). For example, a Class C network address may appear as 192.168.24.11/255.255.255.0.

### Security options

Of the security options settings, the first option (security) is the most important one to get right. It defines the type of security used to give access to the shared file systems and printers to the client computers. (To see some of the fields described here, you need to click the Advanced view.)

- **security** — Sets how password and user information is transferred to the Samba server from the client computer. As noted earlier, it’s important to get this value right. The default value for security (security=user) is different than the default value for security (security=share) in pre-2.0 versions of Samba. If you are coming from an earlier version of Samba and clients are failing to access your server, this setting is a good place to start. Here are your options:
    - **user** — The most common type of security used to share files and printers to Windows 95/98/2000 and Windows NT clients. It is the default set with Samba in the current release. This setting is appropriate if users are doing a lot of file sharing (as opposed to a Samba server used mostly as a print server). It requires that a user provide a user name/password before using the server.
      The easiest way to get this method working is to give a Fedora user account to every client user who will use the Fedora Samba server. This provides basically the same file permissions to a user account through Samba as the same user would get if he or she were logged in directly to Linux.

      > **CAUTION:** Apparently, there is a bug in Windows for Workgroups that causes the password that the user types in to be ignored from a “connect drive” dialog box. Instead, Windows uses the user name and password in effect for the user’s current Windows login session. One way around this problem, although it is clumsy from a security standpoint, is to assign the same user name/password combination for each user on the Fedora computer that they use in Windows.
    - **share** — The share value for security works best for just print sharing or for providing file access that is more public (guest sharing). A client doesn’t need to provide a valid user name and password to access the server. However, the user will typically have a “guest” level of permission to access and change files. See the sidebar describing guest accounts for further information.
    - **server** — The security option that, from the client’s point of view, is the same as *user* security, in that the client still has to provide a valid user name/password combination to use the Samba server at all. The difference is on the server side. With *server* security, the user name/password is sent to another SMB server for validation. If this fails, Samba will try to validate the client using *user* security.
    - **domain** — This security option also, from the client’s point of view, looks the same as *user* security. This setting is used only if the Samba server has been added to a Windows NT domain (using the net join command). When a client tries to connect to the Samba server in this mode, its user name and password are sent to a Windows NT Primary or Backup Domain controller. This is accomplished the same way that a Windows NT server would perform validation. Valid Linux user accounts must still be set up.

- **encrypt passwords** — Controls whether encrypted passwords can be negotiated with the client. This is on (Yes) by default. For *domain* security, this value must be Yes. Later versions of Windows NT (4.0 SP3 or later) and Windows 98 and Windows 2000 expect encrypted passwords to be on. (See the “Setting up Samba clients” section for information on getting clients to use encrypted passwords.)
- **update encrypted** — Allows users who log in with a plain-text password to automatically have their passwords updated to an encrypted password when they log in. Normally, this option is off. It can be turned on when you want an installation using plain-text passwords to have everyone updated to encrypted password authentication. It saves users the trouble of running the `smbpasswd` command directly from the server. After everyone is updated, this feature can be turned off. When this option is on, the encrypt passwords option should be set to no.
- **obey pam restrictions** — Turn this on (Yes) if you want to use PAM for account and session management. Even if activated, PAM is not used if the encrypted passwords feature is turned on (`encrypt passwords = yes`).
- **pam password change** — Indicates to use the PAM password change control flag for Samba. If this is on (Yes), SMB clients will use PAM instead of the program listed in the Password Program value for changing SMB passwords.
- **passwd program** — Indicates which password program to use to change Linux user passwords. By default, `/usr/bin/passwd` is used, with the current user name (`%u`) inserted.
- **passwd chat** — Sets the chat that goes on between the Samba daemon (`smbd`) and the Linux password program (`/usr/bin/passwd` by default) when `smbd` tries to synchronize SMB passwords with Linux user passwords.
- **username map** — This sets the file used to map Samba user names. By default, this file is `/etc/samba/smbusers`.
- **unix password sync** — With this on (Yes), Samba tries to update a user’s Linux user password with his or her SMB password when the SMB password is changed. To do this, SMB runs the `passwd` command as the root user. This is on by default.
- **guest account** — Specifies the user name for the guest account. When a service is specified as Guest OK, the user name entered here will be used to access that service. The account is usually the *nobody* user name.

> **TIP:** Make sure that the guest account is a valid user. (The default of *nobody* should already be set up to work.) With an invalid user as the guest account, the IPC$ connection that lists the shared resources fails.
