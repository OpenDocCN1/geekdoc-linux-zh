
The quick way around these problems is to use only share-level security (which, of course, throws your security right out the window). The other solution is to get passwords up-to-date and make sure that clients are using encrypted passwords (as described in the “Setting up Samba clients” section later in this chapter).

## Configuring Samba with SWAT

The Samba Web Administration Tool (SWAT) is a Web-based interface for configuring Samba. While it’s not quite as easy to use as the Samba Server Configuration window, it does offer more options for tuning Samba and Help descriptions for each option. Also, because SWAT is Web-based, you can configure your system remotely from any Web browser.

> **CAUTION:** Both SWAT and the Samba Server Configuration window configure Samba by modifying the `/etc/samba/smb.conf` file. Different GUI tools can overwrite each other’s settings, sometimes in a way that causes the other tool not to work.
>
> In general, it’s best to make a backup copy of your files before switching GUI tools. Eventually, you should choose one tool and stick with it.

### Turning on SWAT

Before you can use SWAT, you must have the `samba-swat` package installed (type `yum install samba-swat`) and start the `swat` service. To set up SWAT to run from your browser, follow these steps:

- 1. To turn on the swat service, type the following, as root user, from a Terminal window:
  ```bash
  # chkconfig swat on
  ```
- 2. To pick up the change to the swat service, reload data for the running xinetd startup script as follows:
  ```bash
  # service xinetd reload
  ```

If xinetd is not yet installed, you should install it (type `yum install xinetd`). If it is not already running, use `start` instead of `reload`. When you have finished this procedure, use the SWAT program, described in the next section, to configure Samba.

### Starting with SWAT

You can run the SWAT program by typing the following URL in your local browser:

```bash
http://127.0.0.1:901/
```

At this point, the browser will prompt you for a user name and password. Enter the root user name and password. The SWAT window should appear, as shown in Figure 17-5.

> **TIP:** Instead of running SWAT from your local browser, you can run it from another computer on the network by substituting the server computer’s name for `127.0.0.1`. (To allow computers besides the local computer to access the swat service, you must change or remove the `only from = 127.0.0.1` line from the `/etc/xinetd.d/swat` file and reload the xinetd service.) Keep in mind that you are entering clear-text passwords when you connect to the SWAT service, so using this feature outside of the local computer is not particularly secure.

![](img/c78bdcb5b7842a0d73dcc98921f872a2_724_0.png)

**Figure 17-5:** Use SWAT from your browser to manage your Samba configuration.

The rest of this section describes how to use SWAT to create your configuration entries (in `/etc/samba/smb.conf`) and to work with that configuration.

> **CAUTION:** Any time you use a GUI to change a plain-text configuration file (as you do with SWAT), you may lose some of the information that you put in by hand. In this case, SWAT deletes comment lines and rearranges other entries. To protect changes you have made manually, make a backup copy of your `/etc/samba/smb.conf` file before you edit it with SWAT.

### Creating global Samba settings in SWAT

A group of global settings affects how file and print sharing are generally accomplished on a Samba server. They appear under the `[global]` heading in the `/etc/samba/smb.conf` file. To edit global variables, click the **GLOBALS** option on the SWAT window.

While not all of the options available from Samba SWAT are especially useful, those options that are useful are described below. To view and modify your global Samba server settings, click the **GLOBALS** option. Then use the following options.

> **NOTE:** Each option shown relates to the exact parameters used in the `/etc/samba/smb.conf` file. You can refer to the `smb.conf` man page (type `man smb.conf`) to get more information on these parameters.

#### Base options

The following are some general Samba server options:

- **workgroup** — The name of the workgroup associated with the group of SMB hosts. By default in Fedora, the value for this field is **MYGROUP**.
- **realm** — If you are using kerberos authentication, this value indicates the kerberos realm to use. Typically, that is reflected by the hostname of the server providing the service.
- **netbios name** — The name assigned to this Samba server. You can use the same name as your DNS hostname or leave it blank, in which case the DNS hostname is used automatically.
- **netbios alias** — This enables you to set a way of referring to a host computer (an alias) that is different from the host's TCP/IP DNS name.
- **server string** — A string of text identifying the server. This name appears in places such as the printer comment box. By default, it says Samba and the version number.
- **interfaces** — Enables you to set up more than one network interface. This enables Samba to browse several different subnetworks. The form of this field can be *IP Address/Subnetwork Mask*. Or, you could identify a network interface (such as eth0 for the first Ethernet card on your computer). For example, a Class C network address may appear as `192.168.24.11/255.255.255.0`.

#### Security options

Of the security options settings, the first option (security) is the most important one to get right. It defines the type of security used to give access to the shared file systems and printers to the client computers. (To see some of the fields described here, you need to click the Advanced view.)

- **security** — Sets how password and user information is transferred to the Samba server from the client computer. As noted earlier, it's important to get this value right. The default value for security (*security=user*) is different than the default value for security (*security=share*) in pre-2.0 versions of Samba. If you are coming from an earlier version of Samba and clients are failing to access your server, this setting is a good place to start. Here are your options:
- **user** — The most common type of security used to share files and printers to Windows 95/98/2000 and Windows NT clients. It is the default set with Samba in the current release. This setting is appropriate if users are doing a lot of file sharing (as opposed to a Samba server used mostly as a print server). It requires that a user provide a user name/password before using the server.

The easiest way to get this method working is to give a Linux user account to every client user who will use the Fedora Samba server. This provides basically the same file permissions to a user account through Samba as the same user would get if he or she were logged in directly to Linux.

- **share** — The share value for security works best for just print sharing or for providing file access that is more public (guest sharing). A client doesn't need to provide a valid user name and password to access the server. However, the user will typically have a "guest" level of permission to access and change files.
- **server** — The server option that, from the client's point of view, is the same as user security, in that the client still has to provide a valid user name/password combination to use the Samba server at all. The difference is on the server side. With server security, the user name/password is sent to another SMB server for validation. If this fails, Samba will try to validate the client using user security.
- **domain** — This security option also, from the client's point of view, looks the same as user security. This setting is used only if the Samba server has been added to a Windows NT domain (using the `net join` command). When a client tries to connect to the Samba server in this mode, its user name and password are sent to a Windows NT Primary or Backup Domain controller. This is accomplished the same way that a Windows NT server would perform validation. Valid Linux user accounts must still be set up.
- **ads** — This security option causes Samba to act as a domain member in an ADS realm. Kerberos must be installed on the Samba machine to use this option. Samba must also join the ADS realm (see the `net` utility).
- **auth methods** — Sets the authentication method used by the Samba server (`smbd`). Leave the default in most cases. Authentication methods you can choose include anonymous access (guest), relay authentication through winbind (winbind), pre-windbind NT authentication (ntdomain), local lookups based on netbios or domain name (sam), or remote DC authentication of trusted users (trustdomain).
- **encrypt passwords** — Controls whether encrypted passwords can be negotiated with the client. This is on (yes) by default. For domain security, this value must be yes. Later versions of Windows NT (4.0 SP3 or later) and Windows 98 and Windows 2000 expect encrypted passwords to be on. (See the "Setting up Samba clients" section for information on getting clients to use encrypted passwords.)
- **client schannel** — Choose if the client is to require the use of netlogin schannel (yes), offer schannel but doesn't enforce it (auto), or not even offer schannel (no).
- **server schannel** — Choose if the server requires clients the use of netlogin schannel (yes), offers schannel but doesn't enforce it (auto), or doesn't even offer schannel (no). If you set this to no, you must apply the Windows XP `WinXP_SignOSctal.reg` patch available from the Samba project.
