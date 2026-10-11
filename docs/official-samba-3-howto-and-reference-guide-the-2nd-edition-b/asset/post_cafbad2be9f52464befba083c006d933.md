
Windows 200x does not seem to create the `.kerberos.wsp` and `.ldap.tcp` in the default DNS setup. Perhaps this will be fixed later in service packs.

### 6.5 Sharing User ID Mappings between Samba Domain Members

Samba maps UNIX users and groups (identified by UIDs and GIDs) to Windows users and groups (identified by SIDs). These mappings are done by the `tdap` subsystem of Samba.

In some cases it is useful to share these mappings between Samba domain members. **name->id** mapping is identical on all machines. This may be needed in particular when sharing files over both CIFS and NFS.

To use the LDAP `ldap idmap suffix`, set:

```
ldap idmap suffix = ou=idmap,dc=quenya,dc=org
```

See the `smb.conf` man page entry for the `ldap idmap suffix` parameter for further information.

Do not forget to specify also the `ldap admin dn` and to make certain to set the LDAP administrative password into the `secrets.tdb` using:

```
root#   smbpasswd -w ldap-admin-password
```

In place of `ldap-admin-password`, substitute the LDAP administration password for your system.

## 6.6 Common Errors

In the process of adding/deleting/re-adding domain member machine trust accounts, there are many traps for the unwary player and many “little” things that can go wrong. It is particularly interesting how often subscribers on the Samba mailing list have concluded after repeated failed attempts to add a machine account that it is necessary to “reinstall” MS Windows on the machine. In truth, it is seldom necessary to reinstall because of this type of problem. The real solution is often quite simple, and with an understanding of how MS Windows networking functions, it is easy to overcome.

### 6.6.1 Cannot Add Machine Back to Domain

> “A Windows workstation was reinstalled. The original domain machine trust account was deleted and added immediately. The workstation will not join the domain if I use the same machine name. Attempts to add the machine fail with a message that the machine already exists on the network — I know it does not. Why is this failing?”

The original name is still in the NetBIOS name cache and must expire after machine account deletion before adding that same name as a domain member again. The best advice is to delete the old account and then add the machine with a new name. Alternately, the name cache can be flushed and reloaded with current data using the **nbtest** command on the Windows client:

```
C:\> nbtest -R
```

### 6.6.2 Adding Machine to Domain Fails

"Adding a Windows 200x or XP Professional machine to the Samba PDC Domain fails with a message that says, 'The machine could not be added at this time. There is a network problem. Please try again later. Why?'"

You should check that there is an **add machine script** in your *smb.conf* file. If there is not, please add one that is appropriate for your OS platform. If a script has been defined, you will need to debug its operation. Increase the *log level* in the *smb.conf* file to level 10, then try to rejoin the domain. Check the logs to see which operation is failing.

Possible causes include:

- The script does not actually exist, or could not be located in the path specified.
- *Corrective action*: Fix it. Make sure when run manually that the script will add both the UNIX system account and the Samba SAM account.
- The machine could not be added to the UNIX system accounts file */etc/passwd*.
- *Corrective action*: Check that the machine name is a legal UNIX system account name. If the UNIX utility **useradd** is called, then make sure that the machine name you are trying to add can be added using this tool. **Useradd** on some systems will not allow any uppercase characters nor will it allow spaces in the name.

The **add machine script** does not create the machine account in the Samba backend database; it is there only to create a UNIX system account to which the Samba backend database account can be mapped.

### 6.6.3 I Can't Join a Windows 2003 PDC

Windows 2003 requires SMB signing. Client-side SMB signing has been implemented in Samba-3.0. Set *client use spnego* = yes when communicating with a Windows 2003 server. This will not interfere with other Windows clients that do not support the more advanced security features of Windows 2003 because the client will simply negotiate a protocol that both it and the server support. This is a well-known fall-back facility that is built into the SMB/CIFS protocols.

## STANDALONE SERVERS

Standalone servers are independent of domain controllers on the network. They are not domain members and function more like workgroup servers. In many cases a standalone server is configured with a minimum of security control with the intent that all data served will be readily accessible to all users.

## 7.1 Features and Benefits

Standalone servers can be as secure or as insecure as needs dictate. They can have simple or complex configurations. Above all, despite the hoopla about domain security, they remain a common installation.

If all that is needed is a server for read-only files, or for printers alone, it may not make sense to effect a complex installation. For example, a drafting office needs to store old drawings and reference standards. Noone can write files to the server because it is legislatively important that all documents remain unaltered. A share-mode read-only standalone server is an ideal solution.

Another situation that warrants simplicity is an office that has many printers that are queued off a single central server. Everyone needs to be able to print to the printers, there is no need to effect any access controls, and no files will be served from the print server. Again, a share-mode standalone server makes a great solution.

## 7.2 Background

The term *standalone server* means that it will provide local authentication and access control for all resources that are available from it. In general this means that there will be a local user database. In more technical terms, it means resources on the machine will be made available in either *share* mode or in *user* mode.

No special action is needed other than to create user accounts. Standalone servers do not provide network logon services. This means that machines that use this server do not perform a domain logon to it. Whatever logon facility the workstations are subject to is independent of this machine. It is, however, necessary to accommodate any network user so the logon name he or she uses will be translated (mapped) locally on the standalone server to a locally known user name. There are several ways this can be done.

Samba tends to blur the distinction a little in defining a standalone server. This is because the authentication database may be local or on a remote server, even if from the SMB protocol perspective the Samba server is not a member of a domain security context.

Through the use of Pluggable Authentication Modules (PAM) (see Chapter 27, “PAM-Based Distributed Authentication”) and the name service switcher (NSS), which maintains the UNIX-user database, the source of authentication may reside on another server. We would be inclined to call this the authentication server. This means that the Samba server may use the local UNIX/Linux system password database (`/etc/passwd` or `/etc/shadow`), may use a local smbpasswd file, or may use an LDAP backend, or even via PAM and Winbind another CIFS/SMB server for authentication.

## 7.3 Example Configuration

Example 7.3.1 and Section 7.3.2 are designed to inspire simplicity. It is too easy to attempt a high level of creativity and to introduce too much complexity in server and network design.

### 7.3.1 Reference Documentation Server

Configuration of a read-only data server that everyone can access is very simple. By default, all shares are read-only, unless set otherwise in the **smb.conf** file. Example 7.3.1 is the **smb.conf** file that will do this. Assume that all the reference documents are stored in the directory **/export**, and the documents are owned by a user other than nobody. No home directories are shared, and there are no users in the `/etc/passwd` UNIX system database. This is a simple system to administer.

![](img/86d74c6cc862465e3a42e6dc3c90935a_147_0.png)

```
# Global parameters
[global]
    workgroup = MIDEARTH
    netbios name = GANDALF
    security = SHARE
    passdb backend = guest
    wins server = 192.168.1.1
[data]
    comment = Data
    path = /export
    guest only = Yes
```

> I would have spoken more briefly, if I’d had more time to prepare.
> —Mark Twain
