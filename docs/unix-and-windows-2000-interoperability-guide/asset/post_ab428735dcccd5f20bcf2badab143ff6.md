
# CIFS Implementations

So, from the administrator's viewpoint, if you want to share files from a few UNIX servers, what do you do? Install an NFS client on all your Windows clients? Or do you install a CIFS server on your few UNIX servers? Which would require the least amount of administrative overhead? While there may be sites that would choose to standardize on NFS (and this would work well), I would install some kind of CIFS on the UNIX servers. Once you do so, UNIX systems can access their data via NFS, and the Windows-based clients can access the same data via CIFS, their native file sharing protocol. You have fewer installations than the way, and have fewer servers to administer. UNIX systems, because of their wonderful memory model, can easily accommodate multiple protocol stacks. In the case of CIFS, they simply have to accommodate the functionality of the layers above the transport layer: the session, presentation, and application layers.

## 12.3 CIFS Implementations

The SMB protocol, upon which CIFS is based, its first appearance in Microsoft's Lan Manager in 1987. A year later, it appeared in IBM's OS/2 LAN Server. In 1992, SMB became an Open standard and has been a part of Windows for Workgroups, Windows 95, Windows 98, and Windows NT networking as each operating system made its appearance in the marketplace. In 1994, Microsoft released the SMB server code to AT&T; who in turn ported the code to UNIX and made it available to UNIX vendors. Known as Advanced Server for UNIX (ASU), this product was modified, renamed by various users, including Hewlett-Packard and Digital Equipment Corporation (DEC). In 1996, Microsoft changed the name of SMB to CIFS—the terms are frequently used interchangeably—and submitted its specification to the Internet Engineering Task Force (IETF) as an Internet-Draft.

The Open Source movement has produced free software, called Samba, which is a CIFS product designed for UNIX systems. The origins of Samba also go the way back to 1991 as a project of Andrew Triddell, a graduate student at the time in the Computer Sciences Laboratory at Australian National University. Currently spearheaded by a small group called the Samba Team, this free is available for all UNIX implementations. It is open source software, so its licensing is subject to the GNU General Public License. (See Chapter 1 for information on GNU).

In 2000, Hewlett-Packard produced a new product, CIFS/9000, which implements both a CIFS server and a CIFS client on HP-UX 11. The CIFS/9000 Server is based on Samba, version 2.0.6, and provides file and print services to CIFS clients, including Windows 95, 98, NT, 2000, and HP-UX machines running CIFS/9000 Client software. The CIFS/9000 Client enables HP-UX users to mount as UNIX file shares from CIFS file servers, including Windows and HP-UX machines running CIFS/9000 Server. The CIFS/9000 client also offers an optional Pluggable Authentication Module (PAM) that implements the Windows NT LAN (NTLM) authentication protocols. When installed and configured within HP-UX facility, PAM NTLM allows HP-UX users to be authenticated against a Windows authentication

## 12.4 CIFS/9000 Server in a Windows 2000 Domain

To illustrate connecting HP-UX systems with Windows 2000 systems, we will now describe a configuration using CIFS/9000. Given the close relationship this product has with Samba, much will come forth as a result of this overview. In this way, you can extrapolate what needs to be done to employ CIFS in other UNIX offspring.

### 12.4.1 A Vision

If you have a Windows 2000 domain and want to introduce a CIFS/9000 server into your domain, it makes sense to have the Windows 2000 domain controller authenticate requests for resources. The main purpose for doing so is to avoid having to maintain two separate password databases. A client requests a CIFS/9000 resource, and the CIFS/9000 server passes authentication to the domain controller. As we saw in Chapter 11 with NFS, it helps to have user account names match each other; otherwise, you to create a user-mapping file for account names that differ.

It is common, then, for sites to configure their users so that their UNIX account names and their Windows account names match. However, even though authentication takes place at one location—that of the domain controller—you still maintain two separate databases: one for UNIX and for Windows 2000. If you add a user to the UNIX environment, you must add an equivalent user to the Windows 2000 domain. But, what if you run Server for NIS on the domain controller? That way, you can create new accounts for both environments in one location with Active Directory Users and Computers. (See Chapter 10, “Windows Services for UNIX,” for a description of Server for NIS.) By combining CIFS/9000 (configured to use domain security) with Server for NIS, you can effectively unify your HP-UX and Windows 2000 user datbases. Let's see how.

### 12.4.1.1 Configuring CIFS/9000 Server

Complete instructions on setting up the CIFS/9000 server are in Hewlett-Packard’s document Installing and Administering the CIFS/9000 server. This document describes mostly the enhancements HP has made to Samba and refers the reader to another book, Using Samba, by Robert Eckstein, David Collier, and Peter Kelley, for more specific information on actually using Samba itself, CIFS/9000 essentially is. While there are numerous possible CIFS/9000 server configurations, and while your site will probably necessitate a customized solution, I would like to offer the following tips to assist you in setting it up:

- 1. Follow the instructions found in Installing and Administering the CIFS/9000 Server on how to install CIFS/9000.
- 2. Before configuring anything in the smb.conf file, create a dummy user called smbnull with no home directory and group membership of other. This is described in the CIFS/9000 Release Notes and is designed to prevent problems of file access from Windows 2000 clients, among other things.
- 3. Set the guest account smb.conf variable to smbnull in the global section of the smb.conf file. (With CIFS/9000, this file is found in the /etc/opt/samba directory.)
- 4. Modify smb.conf to support, if necessary, the following features: ACL support, case sensitivity for the Client and Server, DOS attribute, print services, and internationalization.
- 5. Before starting the Samba daemons, add your Windows 2000 domain: Go into Active Directory Users and Computers, select your domain, and then select Action→New→Computer. Fill in the necessary information, check the Allow pre-Windows 2000 computers to use this account, and then click on OK. ![img/1c1e7552b53cca88836c695bdb48_208] Figure 12-1 Adding a CIFS/9000 server to a Windows 2000 domain.
- Then, on the CIFS/9000 Server, issue the smbpasswd command. For example:

```
smbpasswd -j book.local -r w2kserv
```
Supply the Windows 2000 domain name as the argument to -j and the name of your domain controller as the argument to -r. This command will create a system password and store it in the /var/opt/samba/private directory as a file with name in the following format: domain_name.server_name.mac. In my example, the name is BOOK.LOCAL.HPUX1.mac. (The Mac extension means that this is a machine account.)

Edit your smb.conf file and specify the following variables:

- security = domain
- netbios name = server_netbios_name
- workgroup = domain_name
- password server = domain_controller_name(s)
- encrypt passwords = yes

For example, my smb.conf contains the following entries for these variables, as well as for a couple of others:

```
[global]
workgroup = BOOK.LOCAL
netbios name = HPUX1
security = DOMAIN
encrypt passwords = Yes
password server = w2kserv
username map = /var/opt/samba/usermap
guest account = smbnull
read only = No
case sensitive = yes
```

As you can see, I specify the file /var/opt/samba/usermap to contain mappings of user accounts whose names differ between the two operating systems. In my test environment, all my user account names match, with the exception of root and administrator. So, in this file, I have only one entry:

```
root = administrator
```

 also specify smbnull for the guest account and case sensitivity.

- Start the Samba daemons smbd and nmbd. With CIFS/9000, you do so by executing the following command:

```
# /opt/samba/bin/startsmb
```
