
## Networking

Either way, the /etc/resolv.conf should look like this:

```
domain mydomain.co.uk
nameserver 127.0.0.1
```

Samba forwards requests that it cannot resolve itself to the DNS forwarding address that was specified during the provisioning step. It uses its own internal DNS server, but can be configured to use an external BIND DNS instead. However, because you get so much for free with the internal one, it probably isn’t worth doing so unless you really need to.

## Testing phase

With the configuration steps completed, we can start the domain controller and perform some tests. Active Directory mode uses a new samba binary instead of the usual smbd. Here, we start it in the foreground while testing:

```
# samba -M single mydomain
Copyright Andrew Tridgell and the Samba Team 1992-2012
samba: using 'single' process model
# host -t SRV _ldap._tcp.mydomain.co.uk
# host -t SRV _kerberos._udp.mydomain.co.uk
```

```
_kerberos._udp.mydomain.co.uk has SRV record 0 100 88 myhost.mydomain.co.uk
# host -t A myhost.mydomain.co.uk
host -t A myhost.mydomain.co.uk
```

Next, test Kerberos (enter the administrator password when requested):
# kinit administrator@MYDOMAIN.CO.UK
Password for administrator@MYDOMAIN.CO.UK:

```
# klist
Ticket cache: FILE:/tmp/krb5cc_0
Default principal: administrator@MYDOMAIN.CO.UK
Valid starting Expires Service principal
08/02/13 16:25:31 09/02/13 02:25:31 krbtgt/MYDOMAIN.CO.UK@MYDOMAIN.CO.UK
renew until 09/02/13 16:25:21
```

At this point, you should be able to see Samba shares and access them:
$ smbclient -L localhost -U%

```
Domain=[MYDOMAIN] OS=[Unix]
Server=[Samba 4.0.3]
Sharename Type Comment
netlogon Disk
sysvol Disk
```

```
IPC$ IPC IPC Service (Samba 4.0.3)
$ smbclient //localhost/netlogon
-UAdministrator%Pa$$w0rd -c 'ls'
Domain=[MYDOMAIN] OS=[Unix]
Server=[Samba 4.0.3]
```

Another service provided by an Active Directory Domain Controller is time synchronisation. While optional, providing this service is highly recommended because Kerberos is highly sensitive to time variations between clients and the server.

The so-called Windows Time Service that a domain controller provides is a Network Time Protocol (NTP) server with extensions for authentication. There’s a number of NTP implementations on Linux, such as ntpd and open-ntpd, but only ntpd version 4.2.6 onwards supports the necessary authentication extensions, and then only if that support has been compiled in (you should check your ntpd version with ntpd --version). A suitably configured ntpd asks Samba to perform any necessary authentication. The ntpd configuration goes in /etc/ntpd.conf. Here is a suitable example:

```
server 127.127.1.0
fudge 127.127.1.0 stratum 12
ntpsigndsocket /var/lib/samba/ntp_signd/
restrict default noserve
```

The important lines, which may not be in an existing ntpd.conf, are the last two. The ntpsigndsocket entry defines the path to the directory where Samba places the socket file through which it will receive authentication requests. The restrict entry tells ntpd that incoming requests need to be authenticated. The socket path is determined by Samba’s configuration, and you can confirm the correct path with:
# samba-tool testparm --verbose --suppress-

![](img/b6e789f7b1bc6629f6c97a3e4beae1de_95_0.png)

The Samba Web Administration Tool (SWAT) is still around, but hasn’t been updated.

```
prompt | grep "ntp signd socket directory"
ntp signd socket directory = /var/lib/samba/ntp_signd
```

Samba creates the socket directory, but it is very important to ensure that it is writable by ntpd. If ntpd runs with a uid/gid of ntp:ntp then you should change the directory's group to ntp also.

Restart ntpd to ensure that any configuration changes are picked up, and then check its log file for a warning that ntpd was configured without the --enable-ntp-signd compile-time configuration option. If you do see that warning, then your ntpd does not support the required authentication mechanism. You would need to obtain the sources for ntpd and rebuild it to include the aforementioned compile-time configuration option. Unfortunately, there is no tool to test NTP authentication from Linux.

To test it from a Windows computer that

# “Whatever your needs, Samba 4 offers a viable open source alternative”

is a domain member, open a command prompt window as the Administrator (to do this, click the "Start" button, type cmd and then right-click the command prompt entry in the search results to select 'Run as administrator') and enter:

```
C:\> w32tm /resync
Sending resync command to local computer
The command completed successfully.
```

Before connecting a Windows client to the new domain, change its network configuration so that it uses Samba's DNS. Also, it is a good idea to manually adjust the client's clock so that it is within a few seconds of the domain controller. If their clocks aren't synchronised, errors may be reported that bear no relationship to the real problem. The Windows time service will keep the clocks synchronised once the client becomes a domain member.

## Domain admin

To add the client to the domain, go to Start > Computer > Right-click > Properties > Change settings. This will display the Computer Name/ Domain Changes dialog, where you should select Domain in the Member Of section and enter the Samba domain name (for example, mydomain) before pressing OK. This should request the administrator account credentials (the username is Administrator and the password is Pa$$w0rd if you have been following our example settings).

Domain administration can be performed locally on the server using the samba-tool command line utility, or remotely from a Windows computer connected to the domain. An administrator, using a suitably configured computer, can run the Active Directory Users and Computers tool.

This offers full control over users and computers, and also functions exactly the same as though it were administering Microsoft's Active Directory.

Adding users to AD is done differently from classic Samba (which uses smbpasswd), but it's more flexible because it can be done from a server command prompt using samba-tool or remotely from Windows with Active Directory Users and Computers.

When Active Directory users are created, they are unrelated to existing users in /etc/passwd because they are given different uid numbers. The assigned uid can be changed, and it is quite straightforward thing to do so:

```
# wbinfo --name-to-sid myuser
S-1-5-21-4099219672-1275272411-291422405-1104 SID_USER (1)
# ldbedit -H idmap.ldb -s 1-5-21-4099219672-1275272411-291422405-1104
```

This allows you to edit an entry from Samba's ID mapping database using your default editor, so that you can change the user's uid (the location of idmap.ldb depends on your installation, but will be something like /var/lib/samba/private or /usr/local/samba/private).

| # editing 1 records |
| 1 # record 1 |
| 2 dn: CN=S-1-5-21-4099219672-1275272411-291422405-1105 |
| 3 cn: S-1-5-21-4099219672-1275272411-291422405-1105 |
| 4 objectClass: sidMap |
| 5 objectSid: AQUAAAAAAAUVAAAA2CBV9NSAoZFWf4RUQQAA== |
| 6 type: ID, TYPE, BOTH |
| 7 xidNumber: 300020 |
| 8 distinguishedName: CN=S-1-5-21-4099219672-1275272411-291422405-1105 |

The value to change is xidNumber, which can be changed to the user's correct uid. The changes will be saved to the database when the edit session is exited.

Setting up file shares can be done in a similar way to classic Samba by adding relevant blocks to smb.conf. You can share [homes] as with classic Samba, but you can go a step further and offer roaming profiles with a [profiles] share:

```
[profiles]
comment = Roaming Profiles
path = /var/lib/samba/profiles
writable = yes
browseable = no
```

In order to configure a user with a roaming profile, use the Active Directory Users and Computers tool to edit the user's settings, and set their profile path to \\mydomain\profiles\%USERNAME%. Following this, the user's profile will be copied between the local disk and the Profiles area on the server when they log in to and out of any client on the domain.

## Quick tip

The release notes for the latest stable release Samba 4.0.22 are available at http://bit.ly/10kq4tc.

![](img/b6e789f7b1bc6629f6c97a3e4beae1de_96_0.png)

Adding users can be done from Windows.

So there you have it. Whatever your needs, whether it's just basic file sharing or through to something more complicated such as a complete Active Directory environment, Samba 4 offers a viable open source alternative to otherwise expensive proprietary options.
