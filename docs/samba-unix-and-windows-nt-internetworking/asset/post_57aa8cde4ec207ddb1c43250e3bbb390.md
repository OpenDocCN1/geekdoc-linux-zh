
in the `/usr/local/samba/private` directory as a file named `<Domain Name>.<Samba Name>.mac`. The `mac` file name extension stands for *machine account*.

![](img/7684008b1d7775727df27d44aed5b3f0_133_0.png)

Figure 10.1: Server Manager

### Example 10.1 Creating a Domain Server Password

```
$ smbpasswd -j <Domain Name> -r <PDC Name>.
```

Now it's time to start the `smbd` and `nmbd` daemons on the server. Samba should log-on to the domain during initialization. You can verify active membership using Server Manager (Figure 10.2).

## Domain Control

Although Samba's domain controller functionality is not quite on a par with Windows NT yet, you may still want to consider running Samba as a domain controller for your Windows 9x clients. One reason is that by using Samba as the domain's authentication service, you can collocate UNIX and NetBIOS namespace administration on the same Windows 9x platform. It may also be that your in-house system administration skills and platform support infrastructure favor running a domain controller under UNIX rather than Windows NT. Whatever the reason, you'll find that Samba will perform adequately as a domain controller in the Windows 9x context. Domain control for Windows NT clients entails additional undocumented protocol support and still lies in the realm of the experimental Samba PDC effort.

To enlist Samba as the domain controller for your Windows 9x domain you'll need to verify that WINS service has been configured and is available (see Chapter 8). You can run WINS under Samba by enabling the `wins support` parameter. If WINS services are provided by another machine, identify the remote server's IP address or DNS name using the `wins server` parameter. Remember that `wins support` and `wins server` are mutually exclusive.

```
wins support = yes
```

or

```
wins server = <IP address or DNS name>
```

Identify the NetBIOS name of the server and the domain name using the netbios name and workgroup parameters respectively.

```
netbios name = <NetBIOS name>
workgroup = <domain name>
```

You will also need to configure the server to act as the domain master browser (see Chapter 9). Remember that in a Windows NT domain controller world, the PDC is also the domain master browser. Enable the server's domain master, local master, and preferred master parameters and set the os level parameter to "65" indicating that Samba is emulating Windows NT Server.

```
os level = 65
domain master = yes
local master = yes
preferred master = yes
```

Next you need to create a netlogon share to support domain logons. This share will be used to store logon scripts and the system policy file, CONFIG.POL (see the "Policies" section later in this chapter). The following is an example netlogon share definition. Make certain that the netlogon share is "read-only" to ensure that the domain's system policies and logon scripts can't be modified by clients:

```
[netlogon]
comment = Network Logon Service
path = /usr/local/samba/lib/netlogon
public = no
writable = no
locking = no
```

Verify the netlogon share configuration by invoking the smbclient command with the -U<username> option. You can include the associated password on the command line by using the "%" character as a delimiter between the username and password:

```
$ smbclient -U <username>[%<password>]
```

If Samba will also be providing a private file store for each client, verify that a homes share is defined in smb.conf (see Chapter 11). The homes share is a special service that provides access to a user's UNIX $HOME directory by referencing the user name when accessing the share. You can also designate that the home directory be mounted as a specified drive letter at login time by setting the logon drive and logon home parameters:

```
[homes]
comment = Home Directories
browseable = no
writable = yes
```

```
logon drive = <drive letter>
logon home = \\ %N\%U
```

Now you're ready to permit domain logins by enabling the domain logons parameter. You'll also need to verify that the security parameter has a value of user and that encrypt passwords is enabled.

```
security = user
encrypt passwords = yes
domain logons = yes
```

![](img/7684008b1d7775727df27d44aed5b3f0_135_0.png)

Figure 10.2: Samba domain membership verification

When Samba logs on to a domain, it receives the same authentication and authorization information that would be sent to a Windows client. The data includes structures like Security Identifiers (SIDs) and domain group membership. In future releases of Samba this information will be used for automatic generation of UNIX UIDs and GIDs. Stay tuned.

## Logon Scripts

In Chapter 6 we looked at how the preexec and postexec parameters can be used to automate execution of commands or scripts when clients connect and disconnect from a share. It is also possible to run a script during domain logon processing using the logon script parameter. Using substitution variables in the value of logon script name, it's possible to invoke different logon scripts depending on connecting client SMB information. For example, by using the %U parameter as part of the logon script name you can identify per user logon scripts. Make sure you use crlf format in your scripts so as not to confuse DOS clients. A sample logon script is listed in Example 10.2. The sample script synchronizes the client's system time with a time server and mounts a shared directory as drive letter S:. Combine the use of logon scripts with preexec and postexec to further tailor domain connect/disconnect processing.

```
logon script = \\ %N\netlogon\scripts\%U.bat
```

### Example 10.2 Sample Logon Script

```
# Sample logon script
ECHO Domain Logon Setup
NET TIME \\<server-name> /YES /SET
NET USE S: \\<server-name>\workspace
```

## Roaming Profiles

Most of us spend too much time artistically tailoring our Windows desktops. Our chosen display background, text fonts, application shortcuts, icons, and screen saver all reflect a bit of our cyber persona. Everything has to be in its proper place on the screen. After putting in so much effort, we all get a little irked when our carefully crafted desktop world doesn't automatically follow us as we move from one workstation to the next.

There is a solution to this dilemma called a roaming profile, a Windows desktop profile that has been stored on a network drive and copied to the local workstation at logon time. The profile itself is a collection of Windows environment settings used in concert with installed applications and folders to create the user's working desktop. Profiles are cached copies of the Windows Registry key HKEY_CURRENT_USER and stored as a file named user.DAT under Windows 9x and NTuser.DAT for Windows NT. The HKEY_CURRENT_USER structure reflects the desktop preferences set by the current logged in user.

The collection of user profiles is commonly stored by user name in a PROFILES directory residing under the system root on the domain controller. When a user logs on to the domain, Windows checks the time stamp of the remote profile stored on the domain controller against a local copy stored on the workstation. The most recent copy is then used to setup the user's initial desktop environment. When the user logs out, the profile is copied back onto the domain controller. Assuming no problems have occurred during domain logout, the most recent copy of the profile will reside on the domain controller and will be available when the user logs on from any domain workstation.

Profiles also provide the system administrator a means for configuring common or default desktop rules for users. If the file extension of the profile file is changed from DAT to MAN, the profile becomes a mandatory profile and will be used to set the initial desktop environment. The end-user can modify the desktop during the session, but those changes will not be reflected in the mandatory profile stored on the domain controller.

Roaming profiles are designated in Samba by the logon path parameter. The default path is to store the profile in the user's home directory. Due to the problem that Windows clients may leave the home directory mounted after user logout, it is recommended to specify an alternate repository for storing roaming profiles. A simple solution is to create a
