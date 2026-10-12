
## Setting the [global] parameters

The [global] section defines Samba parameters that apply to all other configuration sections (that is, services that they define). The default [global] configuration is as follows:

```
[global]
    workgroup = MYGROUP
    server string = Samba Server
    printcap name = /etc/printcap
    load printers = yes
    printing = lprng
    log file = /var/log/samba/%m.log
    max log size = 0
    security = user
    socket options = TCP_NODELAY \
                  SO_RCVBUF=8192 \
                  SO_SNDBUF=8192
    dns proxy = no
```

The following sections show you how to configure each of these parameters.

### workgroup

Set this parameter to the Windows workgroup or Windows NT/2000 domain name that you want Samba to participate in as a node. For example, I use EVOKNOW as the Windows NT/2000 domain name so that I can set workgroup to EVOKNOW. When a Windows 9x or Windows NT/2000 system on my network browses the Network Neighborhood, it sees the Samba server under the EVOKNOW Windows NT/2000 domain. Set this to whatever workgroup or domain name is appropriate for your LAN.

### server string

Set this parameter to provide a description for your Samba server. This description will be visible to Samba clients (such as a Windows 9x machine).

### printcap name

Use this parameter to set the printcap file path. The default value of /etc/printcap should work for you. The /etc/printcap file is used to describe your printer’s capabilities. If you have one or more printers attached to your Linux server and you want to make all of your printers available to the Windows systems on your LAN, set this parameter along with the load printers parameter.

### load printers

Use this parameter to tell Samba to automatically make local printers available to any SMB client computer on the network. Set this to yes if you want to enable this feature; set it to no if you prefer to specify printer configurations in individual configuration sections.

### printing

The printing parameter is used to set the print command. The default value of lprng tells Samba to use the lpr command.

### log file

Use this parameter to set the filename of the Samba log file. The default setting writes a log file per client. This is done using the %m macro, which expands to the client name. For example, if you keep the log file setting as is and access the Samba server from a Windows machine called r2d2, a log file called /var/log/samba/r2d2.log is created.

### max log size

Use this parameter to control the maximum log file size, in kilobytes.

### security

The security parameter is the most important of all the global parameters. Use it to tell Samba how to perform client authentication. The following are the four possible values for security, along with a description of what the Samba server does when security is set to each:

- **user.** The Samba server tells the client to supply a username/password pair for authentication. If you use the same username/password pairs on your Windows systems and Linux systems, set the security parameter to user. For example, if you have a user called joe on a Windows NT/2000 Server and have the same user on the Samba server with the same password, set this parameter to user.
- **share.** The Samba server expects a password with each request for a service. No usernames are required. Use this setting if your Windows systems and the Linux Samba server do not have the same set of username/password pairs.
- **server.** The Samba server tells the client to supply a username/password pair, just like when you set this parameter to user, but the Samba server does not verify the username/password pair itself. It uses another SMB server to authenticate the user. For this reason, when you set security to server, you must also set the password server parameter, which is used to name a SMB server that will be responsible for authentication. If you want to centralize your usernames/passwords for SMB activity on a Windows NT/2000 server, set the password server parameter to point to the Windows NT/2000 server.

![](img/9eb7e89292d2f85707b4d49102c865b7_530_0.png)

If you use a Windows NT/2000 as your password server to do all the authentication for Samba, make sure that you do not have the guest account on the Windows NT/2000 system enabled. If the guest account is enabled, any time that a username/password pair fails because of an incorrect password, Windows NT/2000 will still provide a valid response to the Samba server, because Windows NT/2000 will simply assign guest privileges to the failed authentication attempt and return a success response to the Samba server.

- **Domain.** The Samba server uses the domain controller to authenticate users. Passwords must be transmitted in encrypted format and therefore encrypted passwords option needs to be set to yes.

The default setting for security is user, which means that a client has to supply a plain-text password along with a username. The Samba server verifies this username/password pair by using the /etc/passwd file. However, the later versions of Windows 9x and Windows NT/2000 don't use plain-text (also known as clear-text) passwords, by default. Microsoft decided to use encrypted passwords as part of upgrades to its OS service packs. Because these Windows clients do not supply plain-text passwords, they can't be verified; therefore, the Samba server refuses to service them. To remedy this problem, you have two options:

- Enable plain-text passwords on Windows systems. This option is acceptable if any of the following conditions are true:
  - You already allow plain-text-based services, such as FTP and Telnet, between your Windows machine and a Red Hat Linux server.
  - Your network is not connected to the Internet, so use of plain-text passwords does not pose a great threat to your organization.
  - You just want to get Samba working first and then either deal with encrypted passwords or plan on delegating all authentication tasks to a Windows NT/2000 system in the long run.
- Use encrypted passwords for authentication.

You probably will choose the first option, so it is described next. The details of using encrypted passwords for authentication are provided in the last section of this chapter.

If you are using Windows 98, Windows 95 with Service Pack 3 or later, or Windows NT with Service Pack 3 or later, follow these steps to enable plain-text passwords:

1. Run the Windows Registry editor program called RegEdit by clicking the Start button, choosing Run, entering regedit in the command field, and clicking OK.
2. For Windows 9x, locate the following Registry key:

```
/HKEY_LOCAL_MACHINE
/System
/CurrentControlSet
/Services
/VxD
/VNETSUP
```

For Windows NT/2000 with Service Pack 3 or later, locate the following Registry key:

```
/HKEY_LOCAL_MACHINE
/SYSTEM
/CurrentControlSet
/Services
/Rdr
/Parameters
```

3. After you locate the VNETSUP branch (for Windows 9x) or the Parameters branch (for Windows NT/2000) in the Registry tree, select Edit → New and choose to create a new DWORD value.
4. RegEdit will insert a new DWORD value called New Value #1 in the Registry. Rename this new value EnablePlainTextPassword and double-click this new name.
5. A dialog box pops up, enabling you to set a value for the EnablePlainTextPassword you just created. Enter 1 as the value and close RegEdit as usual.
6. Reboot your Windows system.

This ensures that your Windows system is able to use plain-text passwords for SMB authentication.

### socket options

By default, the socket options parameter in the global configuration section is set to TCP_NODELAY SO_RCVBUF=8192 SO_SNDBUF=8192, which enhances Samba performance on certain platforms. Leave this parameter as is.

### dns proxy

This parameter affects how the Samba suite's built-in Windows Internet Name Server (nmbd) behaves when a Windows system name (NetBIOS
