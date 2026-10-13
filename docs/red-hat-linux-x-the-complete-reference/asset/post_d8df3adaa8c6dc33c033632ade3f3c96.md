
## Tip

Be sure that you have installed all development packages on your system. Development packages contain the key components such as the compiler, GNOME and KDE headers.

First you locate the software - in this case, from apps.kde.com and then you download it to your system.

KonCD is downloaded in a file named koncd-1.0rc2.tar.gz. Then decompress and extract the file using the tar command with the xvzf options, as shown here:

```
tar xvfz koncd-1.0rc2.tar.gz
```

This will create a directory with the name of the software, in this case koncd-1.0rc2. Change to this directory with the cd command:

```
cd koncd-1.0rc2
```

Issue the command ./configure. This generates a compiler configuration for your particular system.

```
./configure
```

Compile the software with the make command:

```
make
```

Then install the program with the make install command:

```
make install
```

Most KDE and GNOME software will also place an entry for the program in the appropriate menus - for example, a KonCD entry will be placed in the KDE Applications menu. You can then run KonCD from the menu entry. You could also open a terminal window and enter the program's name.

## Security Configuration

Once you have installed your Linux system, you should carry out some basic security measures to protect your system from outside attacks. Systems connected to the Internet are open to attempts by outside users to gain unauthorized access. This usually takes the following forms:

- Trying to break into the system
- Having broken in, changing or replacing system files with hacked or corrupt versions
- Attempting to intercept communications from remote users
- Changing or replacing messages sent to or from users
- Pretending to be a valid user

Firewalls, intrusion protection, encryption, data integrity, and authentication are ways of protecting against such attacks.

- A firewall prevents any direct unauthorized attempts at access.
- Intrusion detection checks the state of your system files to see if they have been tampered with by someone who has broken in.
- Encryption protects transmissions by authorized remote users, providing privacy.
- Integrity checks such as modification digests guarantee that messages and data have not been intercepted and changed or substituted en route.
- Authentication methods such as digital signatures can verify that the user claiming to send a message or access your system is actually that person.

## Security Services

Red Hat includes several security services for protecting your system and your network transmissions (see Table 4-3). Using GNU Privacy Guard (GPG) you can encrypt your e-mail messages or files you want to send, as well as letting you sign them with an encrypted digital signature authenticating that the message was sent by you (see Chapter 16). The digital signature also includes encrypted modification digest information that provides an integrity check, allowing the recipient to verify that the message received is the original and not one that has been changed or substituted.

A good foundation for your network security is to set up a Linux system to operate as a firewall for your network, protecting it from unauthorized access (see Chapter 19). You can use a firewall to implement either packet filtering or proxies. Packet filtering is simply the process of deciding whether a packet received by the firewall host should be passed on into the local system or network. The firewall package currently in use is Netfilter (iptables). Older distribution versions release an earlier version called ipchains. To implement a firewall, you simply provide a series of rules to govern what kind of access you want to allow on your system. If that system is also a gateway for a private network, the system's firewall capability can effectively protect the network from outside attacks. You can provide a simple configuration for your own system using redhat-config-securitylevel as described in Chapter 4.

### Table 4-3: Security Applications

| Applications | Description |
|---|---|
| GNU Privacy Guard (GPG) | Encryption and digital signatures (Chapter 16) www.gnupg.org |
| Netfilter (iptables) | Firewall packet filtering (Chapter 19) www.netfilter.org |
| Squid | Web proxy server (Chapter 23) www.squid-cache.org |
| Open-SSH | Secure Shell encryption and authentication for remote access (Chapter 18) www.openssh.org |
| Kerberos | User authentication for access to services (Chapter 18) web.mit.edu/kerberos/www/ |
| Pluggable Authorization Modules (PAM) | Authentication management and configuration (Chapter 28) |
| Shadow passwords | Password encryption (Chapter 28) |
| Lightweight Directory Access Protocol (LDAP) | User management and authorization (Chapter 28) www.openldap.org |
| authconfig-gtk | Red Hat tool to enable and configure authentication tools: Kerberos, LDAP, and shadow passwords |

Outside users may also try to gain unauthorized access through any Internet services you may be hosting, such as a Web site. In such a case, you can set up a proxy to protect your site from attack. For Linux systems, use Squid proxy software to set up a proxy to protect your Web server (see Chapter 20).

To further control access to your system is to provide secure user authentication with encrypted passwords, a Lightweight Directory Access Protocol (LDAP) service, and Pluggable Authentication Modules (PAM) (see Chapter 28). User authentication can be further controlled for certain services by Kerberos servers (see Chapter 18). Kerberos authentication provides another level of security whereby individual services can be protected, allowing use of a service only to users who are cleared for access. LDAP and Kerberos are all enabled and configured with authconfig-gtk (Authentication in the System Settings menu or window).

To protect remote connections from hosts outside your network, transmissions can be encrypted. For Linux systems, you can use the Secure Shell (SSH) suite of programs to encrypt any transmissions, preventing them from being read by anyone else (see Chapter 18). The SSH programs are meant to replace the remote tools such as rsh and rcp (see Chapter 15), which perform no encryption.

The IPsec protocol also provides encryption of network transmissions, but integrated into the IP packet structure (see Chapter 17). With IPsec you can both encrypt and authenticate transmissions, ensuring that they were not intercepted and tampered with. With IPsec you can implement Virtual Private Networks (VPN), using encrypted transmissions to connect one local network to another using a larger network like the Internet. Red Hat also provides a third-party solution for VPNs called CPIE (see Chapter 5).

You can find the latest news on security issues at the Red Hat Web site (www.redhat.com) along with other Linux sites like Linux Security (www.linuxsecurity.com), Linux Weekly News (lwn.net), and Linux Today (linuxtoday.com).

Note: Numerous older security applications are also available for Linux such as COPS (Computer Oracle and Password System) to check password security; Tiger, which scans your system etc.

## Authentication Configuration

To confirm user identities, your network may provide several authentication services (see Chapter 28). These can be enabled on your system using authconfig-gtk (see Figure 4-6). You can invoke authconfig-gtk by selecting Authentication from the System Settings menu. authconfig-gtk consists of two panels, User Information and Authentication. Configuration consists primarily of specifying the address of service's server on your network. The User Information panel is used for services like NIS (see Chapter 36) and LDAP (see Chapter 28), which maintain configuration information about systems and users on your network. The Authentication panel lists services for authenticating users. The Shadow and MD5 Password options are normally selected already and provide password protection (see Chapter 28). If your network also maintains LDAP, Kerberos (see Chapter 18), and SMB authentication servers (see Chapter 37), you can enable support for them here, specifying their servers and domains.

![](img/32a48d8db4c23e6e2eb70d1e5034c976_80_0.png)

Figure 4-6: Authentication with authconfig-gtk
