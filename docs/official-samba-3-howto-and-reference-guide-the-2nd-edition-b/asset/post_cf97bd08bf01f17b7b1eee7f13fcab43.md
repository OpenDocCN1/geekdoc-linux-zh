
![](img/86d74c6cc862465e3a42e6dc3c90935a_115_0.png)

## 4.6.2 Security Mode and Master Browsers

There are a few comments to make in order to tie up some loose ends. There has been much debate over the issue of whether it is okay to configure Samba as a domain controller that operates with security mode other than user-mode. The only security mode that will not work due to technical reasons is share-mode security. Domain and server mode security are really just a variation on SMB user-level security.

Actually, this issue is also closely tied to the debate on whether Samba must be the DMB for its workgroup when operating as a domain controller. In a pure Microsoft Windows NT domain, the PDC wins the election to be the DMB, and then registers the DOMAIN<1B> NetBIOS name. This is not the name used by Windows clients to locate the domain controller, all domain controllers register the DOMAIN<1C> name and Windows clients locate a network logon server for searching for the DOMAIN<1C> name. A DMB is a Domain Master Browser — see Chapter 9, “Network Browsing”, Section 9.4.1: Microsoft PDCs expect to win the election to become the DMB, if it loses that election it will report a continuous and rapid sequence of warning messages to its Windows event logger complaining that it has lost the election to become a DMB. For this reason, in networks where a Samba server is the PDC it is wise to configure the Samba domain controller as the DMB.

![](img/86d74c6cc862465e3a42e6dc3c90935a_115_1.png)

Now back to the issue of configuring a Samba domain controller to use a mode other than *security = user*. If a Samba host is configured to use another SMB server or domain controller in order to validate user connection requests, it is a fact that some other machine on the network (the *password server*) knows more about the user than the Samba host. About **99** percent of the time, this other host is a domain controller. Now to operate in domain mode security, the *workgroup* parameter must be set to the name of the Windows NT domain (which already has a domain controller). If the domain does not already have a domain controller, you do not yet have a domain.

Configuring a Samba box as a domain controller for a domain that already by definition has a PDC is asking for trouble. Therefore, you should always configure the Samba domain controller to be the DMB for its domain and set *security = user*. This is the only officially supported mode of operation.

## 4.7 Common Errors

### 4.7.1 "s" Cannot Be Included in Machine Name

A machine account, typically stored in /etc/passwd, takes the form of the machine name with a “$” appended. Some BSD systems will not create a user with a “$” in the name. Recent versions of FreeBSD have removed this limitation, but older releases are still in common use.

The problem is only in the program used to make the entry. Once made, it works perfectly. Create a user without the “$”. Then use *vipw* to edit the entry, adding the “$”. Or create the whole entry with vipw if you like; make sure you use a unique user login ID.

> NOTE
> The machine account must have the exact name that the workstation has.

> NOTE
> The UNIX tool *vipw* is a common tool for directly editing the /etc/passwd file. The use of vipw will ensure that shadow files (where used) will remain current with the passwd file. This is important for security reasons.

### 4.7.2 Joining Domain Fails Because of Existing Machine Account

“I get told, ‘You already have a connection to the Domain...’ or ‘Cannot join domain, the credentials supplied conflict with an existing set...’ when creating a Machine Trust Account.”

This happens if you try to create a Machine Trust Account from the machine itself and already have a connection (e.g., mapped drive) to a share (or IPC$) on the Samba PDC. The following command will remove all network drive connections:

```
C:\> net use * /d
```

This will break all network connections.

Further, if the machine is already a “member of a workgroup” that is the same name as the domain you are joining (bad idea), you will get this message. Change the workgroup name to something else — it does not matter what — reboot, and try again.

### 4.7.3 The System Cannot Log You On (C00019B)

“I joined the domain successfully but after upgrading to a newer version of the Samba code I get the message, ‘The system cannot log you on (C00019B). Please try again or consult your system administrator when attempting to logon.’”

This occurs when the domain SID stored in the secrets.tdb database is changed. The most common cause of a change in domain SID is when the domain name and/or the server name (NetBIOS name) is changed. The only way to correct the problem is to restore the original domain SID or remove the domain client from the domain and rejoin. The domain SID may be reset using either the net or rpcclient utilities.

To reset or change the domain SID you can use the net command as follows:

```
root# net getlocalsid 'OLDNAME'
root# net setlocalsid 'SID'
```

Workstation Machine Trust Accounts work only with the domain (or network) SID. If this SID changes, domain members (workstations) will not be able to log onto the domain. The original domain SID can be recovered from the secrets.tdb file. The alternative is to visit each workstation to rejoin it to the domain.

### 4.7.4 The Machine Trust Account Is Not Accessible

“When I try to join the domain I get the message, ‘The machine account for this computer either does not exist or is not accessible.’ What’s wrong?”

This problem is caused by the PDC not having a suitable Machine Trust Account. If you are using the `add machine` script method to create accounts, then this would indicate that it has not worked. Ensure the domain admin user system is working.

Alternatively, if you are creating account entries manually, then they have not been created correctly. Make sure that you have the entry correctly for the Machine Trust Account in `smbpasswd` file on the Samba PDC. If you added the account using an editor rather than using the `smbpasswd` utility, make sure that the account name is the machine `NetBIOS` name with a “$” appended to it (i.e., computerName$). There must be an entry in both the POSIX UNIX system account backend as well as in the `SambaSAMAccount` backend. The default backend for Samba-3 (i.e., the parameter `passdb backend` is **not** specified in the `smb.conf` file, or if specified is set to `smbpasswd` are respectively the `/etc/passwd` and `/etc/samba/smbpasswd` (or `/usr/local/samba/lib/private/smbpasswd` if compiled using Samba Team default settings). The use of `/etc/passwd` can be overridden by alternative settings in the `NSS /etc/nsswitch.conf` file.

Some people have also reported that inconsistent subnet masks between the Samba server and the NT client can cause this problem. Make sure that these are consistent for both client and server.

### 4.7.5 Account Disabled

> “When I attempt to log in to a Samba domain from a NT4/W200x workstation, I get a message about my account being disabled.”

Enable the user accounts with `smbpasswd -e username`. This is normally done as an account is created.

### 4.7.6 Domain Controller Unavailable

> “Until a few minutes after Samba has started, clients get the error ‘Domain Controller Unavailable’”

A domain controller has to announce its role on the network. This usually takes a while. Be patient for up to 15 minutes, then try again.

### 4.7.7 Cannot Log onto Domain Member Workstation After Joining Domain

After successfully joining the domain, user logons fail with one of two messages: one to the effect that the domain controller cannot be found; the other claims that the account does not exist in the domain or that the password is incorrect. This may be due to incompatible settings between the Windows client and the Samba-3 server for `schannel` (secure channel) settings or `smb signing` settings. Check your Samba settings for `client schannel`, `server schannel`, `client signing`, `server signing` by executing:
