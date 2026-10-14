
# Introducing a global tech brand
that promises to change the way
you consume technology

![](img/b6e789f7b1bc6629f6c97a3e4beae1de_88_0.png)

# Covering the
latest new
technology

- in depth
- in detail
- fully tested gear

![](img/b6e789f7b1bc6629f6c97a3e4beae1de_88_1.png)

![](img/b6e789f7b1bc6629f6c97a3e4beae1de_88_2.png)

# THE HACKER'S MANUAL
2015

# Networking

The true sign of a Linux master is expertise on the desktop, the command line and, most crucially, the network. The skills to mesh machines together, even those running different operating systems, are vital – a lone PC is the rarest of creatures in this day and age.

- Samba: Dancing with Windows ........................................................ 92
- Networking: The basics ................................................................. 98
- Wireshark: Analyse traffic .......................................................... 102
- Networking: Build a router ........................................................ 106
- Deluge: Set up a torrent server .................................................. 110
- Docker: Build containers ........................................................... 114
- Zabbix: Monitor your network .................................................... 118

# Samba

# Dancing with Windows

The Windows interoperability suite for Linux that boasts Active Directory support. Let’s take it for a spin.

We all love our Linux boxes, but most of us at some point need to co-exist on a network with Windows machines, and know Samba as the thing that enables sharing filesystems between Linux and Windows. But it does much more than that and, with version 4, is fully compatible with Microsoft’s Active Directory. This is a big thing – Samba has long been able to act as a Windows NT 4.0 Domain Controller, or

> “Samba 4 fully implements the Active Directory domain controller functionality”

join an existing Windows NT 4.0 Domain but, with the release of Windows 2000, Microsoft

started moving away from NT Domain controllers to its new Active Directory, widening the gap between the Linux and Windows ecosystems. Samba version 4 and upwards provides the long-awaited remedy to this issue by being fully compatible with Active Directory. It fully implements the Active Directory domain controller functionality, making it an effective

replacement for the equivalent functions in Microsoft's Windows Server product line.

Samba is an open source implementation of the Server Message Block, or SMB, protocol. This is an application-layer network protocol that was originally developed by IBM to provide shared access to files and printers. Microsoft extended its implementation of SMB to support authentication using its own NT LAN Manager (NTLM) and, later, NTLMv2 protocols. It called this implementation the Common Internet File System, or CIFS. Further extensions, including support for symbolic links, were released as SMB2 with Windows Vista.

Samba has supported SMB2 since version 3.6. Microsoft introduced SMB2.1 with Windows 7 and SMB3 with Windows 8. It calls the differing versions of the protocol dialects, so CIFS and SMB2 are dialects of the SMB protocol. While these dialects are proprietary, their specifications are publicly available.

One of the outcomes of Microsoft's settlement with the European Courts in 2004 was the release of full documentation for network authentication with Active Directory. This led to the development of version 4 of Samba, with Microsoft itself being involved in the testing.

(LDAP) versions 2 and 3. Kerberos and DNS. Samba uses its own LDAP implementation called ldb; it does not support using OpenLDAP for Active Directory.

So there are now two ways to use Samba – one is to use it how it's always been used (classic Samba), which can either operate as a domain member or standalone, and is all that you need to set up basic shares. The other way is to use Samba as a fully-fledged ADDC. The way you use Samba will depend on your needs, but the first thing that needs to be done is to install it. Most distributions should have it in their repositories. The other option is to build it from source, downloaded from www.samba.

> “The way you use Samba will depend on your needs”

org/samba/download. Once installed, Samba's configuration file is called smb.conf, and will normally be found in a subdirectory, such as /etc/samba. The simplest configuration to use is a standalone public share:

```
[global]

server string = Samba Server Version

%v

# Treat unknown users as a guest
(where permitted)
security = user
map to guest = Bad User

[tmp]
path = /tmp
read only = No
browseable = Yes
guest ok = Yes
force user = nobody
force group = nobody
create mask = 0755
directory mask = 0755
```

This will make /tmp on the server available as a Samba share over TCP/IP. The use of security = user and map to guest allows guest shares to operate similarly to the deprecated security = share mode that existing Samba administrators may be familiar

with. A user with a Windows username that Samba doesn't recognise will not need to provide credentials to access the share, and they will be authenticated as the guest user.

Any files they write there will have their user and group ID set to 'nobody'. However, if the username is known to Samba, then the user will be prompted for their password. This might seem weird, but it is consistent with the way Windows works. Start the Samba daemon, smbd, to make this share accessible on Windows. To access it, simply use Windows Explorer to browse to the Samba server (you can use either its name or IP address).

# Add/Remove NetBIOS

There has been a networking protocol that has long been associated with Windows networking and, therefore, is an integral part of the Samba suite: NetBIOS. These days, NetBIOS generally refers to the NetBIOS over TCP/IP protocol, which is considered a legacy protocol. It offers name resolution, file and printer sharing with devices that do not have DNS capabilities.

It used to be essential in a Windows network, but is no longer necessary unless older versions of Windows are involved, but you still need it if you want clients running OSes prior to Windows 2000 to be able to access your shares. If you don't want to include NetBIOS, the following additions to the [global] section of smb.conf make this explicit:

```
[global]
# disable NetBIOS
 disable netbios = yes
 smb ports = 445
```

Should you need it, however, enabling NetBIOS requires other changes to smb.conf:
[global]

```
# NetBIOS identification
workgroup = WORKGROUP
netbios name = MYHOST
wins support = Yes
```

This tells Samba to use NetBIOS to make itself known to the Windows network in its default workgroup (Windows machines default to a workgroup called WORKGROUP) and to act as a WINS server. The NetBIOS name is the equivalent of a host name – it doesn't need to be the same as the host name, but that is customary. WINS is the Windows Internet

# Quick tip

You do not need to restart or signal Samba when modifying smb.conf because it automatically detects changes.

# SMBFS and CIFS

Two virtual filesystem implementations on Linux allow mounting of SMB shares: SMBFS and CIFS. The latter is the newer implementation and is built into the kernel. The user-space tools that you need to use CIFS were originally part of Samba but are now a separate package that's called cifs-utils.

The original SMBFS, which is also part of the Samba suite, has been deprecated – you should use CIFS to mount Samba filesystems. The upshot of this is that, if you just want to mount Windows shares on your Linux box, you don't need Samba. Mounting a Windows share is as simple as:

mount -t cifs -o username=myuser,password=mypass //myserver/myshare /mnt

The difference between CIFS and SMB can be a little bit confusing, because the CIFS dialect is newer than SMB but older than SMB2, whereas

CIFS is newer than SMBFS and supports SMB, CIFS and the newer SMB2 and SMB3 dialects. For further details, see the client guide. http://pserver.samba.org/samba/ftp/cifs-cvs/linux-cifs-client-guide.pdf

The SMB and CIFS protocol specifications are published at http://msdn.microsoft.com/en-us/library/cc246482.aspx and http://msdn.microsoft.com/en-us/library/ee442092.aspx.
