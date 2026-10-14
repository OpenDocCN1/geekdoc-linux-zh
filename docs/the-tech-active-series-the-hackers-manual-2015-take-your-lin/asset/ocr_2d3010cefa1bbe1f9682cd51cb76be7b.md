# # Networking

![](bbox=[0.06, 0.112, 0.633, 0.326])

# ### Strange things can happen when clocks aren't synchronised!

Name Service, Microsoft’s implementation of a NetBIOS Name Service, and it provides a similar service for NetBIOS names that a DNS provides for domain names (mapping host names to network addresses). Name lookups will resolve without a WINS server, but only within the local subnet – if a client is unable to resolve a NetBIOS name using a WINS server then it will resort to broadcasting “where are you?” messages on the network. This is one reason why sysadmins hate NetBIOS, and why you should disable it unless you really need it. You can also read plenty on the internet about how NetBIOS is insecure.

If you need NetBIOS, the final piece required to support it is to run Samba’s **nmbd** process as well as its **smbd** process. It is **nmbd** that provides the NetBIOS naming and WINS services.

It’s worth understanding how connections are made from the client side. Prior to Windows 2000, connections were only made via NetBIOS, which connects to port 139 on the server. Starting with Windows 2000, connections are made using both NetBIOS and TCP/IP, the latter connecting to port 445 on the server. The client closes its NetBIOS connection on port 139 if the server responds to the TCP/IP connection. As you would expect, shares can be configured so that authentication is required to access them. This requires a database of users to authenticate.

# ## Password management

This is the first area where the Active Directory setup differs from the classic setup. Classic Samba uses its own password database containing encrypted passwords, but because file permissions relate to Unix users and groups, these are directly related to the users on the server. Active Directory users are not related to Unix users (more on this later). To add a user to classic Samba:

> > “You can read plenty on the internet on how NetBIOS is insecure.”

```
smbpasswd -a myuser
New SMB password:
```

# ## Quick tip

Upgrading users should note that the **smbpasswd** file has changed internally, and is therefore not portable between Samba 3.x and Samba 4.

```
RefType new SMB password:
Forcing Primary Group to 'Domain Users' for myuser
Forcing Primary Group to 'Domain Users' for myuser
Added user myuser.
```

Note that once a user has been added to Samba, Windows will require their password to be entered – even for guest shares. Adding a user-specific share, like a home directory, can be achieved with an entry in **smb.conf**:

```
[myuser]
    comment = %U home directory
    writable = yes
    valid users = myuser
    path = %H
```

or, more generally, using the special **[homes]** share, which creates a home share for each user. When a user attempts to connect to a share, Samba looks for an explicit share definition like the one above. If none is found, but a **[homes]** share exists, then that will be used like a template to create the share the user requested. A suitable example is shown below; the browsable entry prevents **[homes]** appearing when the share is browsed.

```
[homes]
    comment = %U home directory
    writable = yes
    browsable = no
```

Another special kind of share is **[printers]**. As you might expect, this allows Windows clients to use printers attached to the Samba server. It uses CUPS to spool raw print jobs, which means that the client needs to have an appropriate printer driver installed. It’s this that converts into the raw data that the printer can process. Printing requires a **spool** directory that has its sticky bit set:

# ## Windows 7 test client

A computer running Windows is required to fully evaluate Samba 4’s Active Directory capabilities. We installed Windows 7 Ultimate with Service Pack 1 along with the Remote Server Administration tools.

From those tools, the one you need is Active Directory Users and Computers (the executable name is **dsa.msc**). Refer to the relevant Microsoft web pages to find more information about installing these:

**Windows 7 Service Pack 1:**
www.microsoft.com/en-us/download/details.aspx?id=5842

**Windows 7 RSAT:**
www.microsoft.com/en-gb/download/details.aspx?id=7887

If you want the Windows machine to respond to ICMP Ping requests, you will need to add an appropriate rule to the Windows firewall (or completely disable the firewall).

To add a rule, go to ‘Start > Control Panel > System and Security > Windows Firewall > Advanced Settings > Inbound Rules > New Rule’. Create a custom rule for the ICMPv4 protocol. Remember that the Home and Starter versions of Windows are unable to join a domain.

![](bbox=[0.641, 0.78, 0.809, 0.932])

For Active Directory Users and Computers search for ‘dsa.msc’ and run it as an administrator.