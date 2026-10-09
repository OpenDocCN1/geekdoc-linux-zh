
## Add or modify Samba users

machines. Change the description of the server if you like. Click the **Security** tab and make sure **Authentication Mode** is set to **User**; you do not need to specify an Authentication Server or a Kerberos Realm. If you are using Windows 98 or later, set **Encrypt Passwords to Yes.** When you specify a username in the Guest Account, anyone logging in on the Samba server as **guest** maps to that user's ID. Click **OK**.

Select **menubar: Preferences→Samba Users** to display the Samba Users window (Figure 23-3). If the user you want to log in as is not listed in this window, click **Add User.** When you have the proper permissions, the Create New Samba User window displays a combo box labeled **Unix Username** that allows you to select a Linux user; otherwise, your username is displayed as the Unix Username. The Windows Username is the Windows username that you want to map to the specified Linux (UNIX) username. The Samba Password is the password this user or Windows enters to gain access to the Samba server.

If Sam's username is **sam** on both the Linux and Windows systems, you would select **sam** from the Unix Username combo box and enter **sam** in the Windows Username text box. If his username were **sls** under Linux and **sam** under Windows, you would select **sls** from the Unix Username combo box and enter **sam** in the Windows Username text box. Finally you would enter Sam's Windows password in the two Samba Password text boxes. Click **OK** to close the Create New Samba User window, then click **OK** to close the Samba Users window.

### User map

If you are mapping a Windows username to a *different* Linux username, you must add the following **username map** (page 843) parameter to the **[global]** section of /etc/samba/smb.conf (page 839):

```
username map = /etc/samba/smbusers
```

Without this line in smb.conf, Samba will not consult the user map file.

### Linux shares

Next you need to add a **share**, which is the directory hierarchy you export from the server (Linux) system to the client (Windows) system. Click the plus sign (+) on the toolbar to display the Basic tab of the Create Samba Share window (Figure 23-4). In

![](img/243613168ac865b539f12460d966088e_895_0.png)

**Figure 23-4** Create Samba Share window, Basic tab

the text box labeled **Folder**, enter the absolute pathname of the directory you want to share (*(/tmp* is an easy directory to practice with). Enter a description if you like. It can be useful to enter the Linux hostname and the pathname of the directory you are sharing here. Put a tick in the check box labeled **Writable** if you want to be able to write to the directory from the client machine; putting a tick in the check box labeled **Visible** allows the share to be seen (browsed) from the client machine. Click the Access tab and specify whether you want to limit access to specified users or whether you want to allow anyone to access this share. Click **OK**. Close the Samba Server Configuration window.

You should now be able to access the share from a Windows machine (page 835). There is no need to start or restart the Samba server.

**Troubleshooting** If the server does not work properly, see “Troubleshooting” on page 846.

## You do not need to restart Samba when you change smb.conf

Samba rereads its configuration files each time a client connects. Unless you change the **security** parameter (page 843), you do not need to restart Samba when you change **smb.conf**.

## smb.conf: MANUALLY CONFIGURING A SAMBA SERVER

The */etc/samba/smb.conf* file controls most aspects of how Samba works and is divided into sections. Each section begins with a line that holds some text between brackets ([...]). The text within the brackets identifies the section. Typical sections are

- `[global]`      Defines global parameters
- `[printers]`    Defines printers
- `[homes]`      Defines shares in user home directories
- `[share name]`    Defines a share (you can have more than one of these sections)

**smb.conf** As installed under Fedora/RHEL, the **smb.conf** sample configuration file contains extensive comments and commented-out examples. Comment lines start with either a hashmark (#) or a semicolon (;). The sample file uses hashmarks to begin lines that are intended to remain as comments. Semicolons begin lines you might want to mimic or use as is by removing the semicolons.

**Basic *smb.conf* file** Following is a basic *smb.conf* file. It depends on default values for many parameters. To make the code clearer, important default values are written as comments beginning with a semicolon as they are in the default *smb.conf* file. To make the system more secure, change the default **server string** to eliminate the Samba version number; this value might aid hackers in penetrating the system. The **hosts allow** and **hosts deny** parameters are not required. When included, they prevent systems other than those listed from contacting the Samba server. If you uncomment these lines, replace 192.168.206.180 with the IP address of the system you want to allow to connect to the Samba server. You must open the firewall (page 836) and start the **smb** and **nmb** services (page 836) before a client can contact the server.

```bash
$ cat /etc/samba/smb.conf

[global]
    workgroup = MGS
    server string = Samba Server Version %v
    log file = /var/log/samba/log.%m
    max log size = 50
    ;   hosts allow = 127.0.0.1, 192.168.206.180
    ;   hosts deny = ALL
    ;   security = user
    ;   encrypt passwords = YES
    ;   guest ok = NO
    ;   guest account = nobody

[homes]
    comment = Home Directories
    read only = NO
    browsable = NO

[tmp]
    comment = Temporary Directory
    path = /tmp
    read only = NO
    guest ok = YES
    ;   available = YES
    ;   browsable = YES
```

**The [homes] share** The sample *smb.conf* file includes the **[homes]** share, which allows users to share their Linux home directories with a Windows machine. The default *smb.conf* file includes the same share. This share causes each user's home directory to be shared with the specified parameters. The pathname of the share is **_username_**; Sam's share on **plum** would be **/plum/sam**. The default settings, which are used in the file shown above, prevent users other than the owners from browsing or accessing home directories while allowing logged-in owners full access.

**SELinux** If the system is running SELinux with a targeted policy and you want to allow users to share their home directories as explained in this section, you must modify the SELinux policy to allow this access. You can use **system-config-selinux** (page 475) to allow this access: In the Booleans tab, **samba** module, put a tick mark adjacent to **Allow samba to share users home directories.**

### Defining a share

- The **tmp** share in the preceding **smb.conf** file enables a user on a *Windows* system to be able to read from and write to the **/tmp** directory on the server. The name of the share under *Windows* is **tmp**; the path under *Linux* is **/tmp**. Any *Windows* user who can log in on Samba, including **guest**, can read from and write to this directory, assuming the user’s *Linux* permissions allow it. To allow a user to log in on Samba, you must run **smbpasswd** (page 831). The **browsable** parameter, which defaults to **YES**, causes the share to appear as a share on the server. The *Linux* permissions that apply to a *Windows* user using Samba are the same permissions that apply to the *Linux* user that the *Windows* user logs in as or maps to.

### Troubleshooting

- Follow the steps in “*Prerequisites*” on page 836 and add users and passwords as necessary (page 831). From a *Windows* machine, you should now be able to access the share you just created (page 835). If the server does not work properly, see “*Troubleshooting*” on page 846.

## PARAMETERS IN THE **smb.conf** FILE

The **smb.conf man** page lists all the parameters you can set in **smb.conf**. The following sections identify some of the parameters you might need to change.

### GLOBAL PARAMETERS

- **interfaces**: A space-separated list of networks Samba listens on. Specify as interface names (such as **lo** and **eth0**) or as IP address/net mask pairs (page 483).
    - *Default:* all active interfaces except 127.0.0.1

- **server string**: The string the client (*Windows*) machine displays in various places. Within the string, Samba replaces **%v** with the Samba version number and **%h** with the hostname of the server. To make the system more secure, eliminate the Samba version number; this value might aid hackers in penetrating the system.
    - *Default:* Samba %v
    - Fedora/RHEL: Samba Server Version %v

- **workgroup**: The workgroup the server belongs to. Set to the same workgroup as the *Windows* clients that use the server. This parameter controls the domain name that Samba uses when security (page 843) is set to **DOMAIN**.
    - *Default:* **WORKGROUP**
    - Fedora/RHEL: MYGROUP

### SECURITY PARAMETERS

- **encrypt passwords**: **YES** accepts only encrypted passwords from clients. *Windows* 98 and *Windows* NT 4.0 Service Pack 3 and later use encrypted passwords by default. This parameter uses **smbpasswd** to authenticate passwords unless you set **security** to **SERVER** or **DOMAIN**, in which case Samba authenticates using another server.
    - *Default:* **YES**
