
of a package. If the value is incorrect, the package has been tampered with. Some packages provide just digest values, allowing only integrity checks. In the next example, the user checks whether the freeciv package has been tampered with. The `--nosignature` option says not to perform authentication, doing the integrity check only.

```
$ rpm -K --nosignature xvidcore-1.2.0-4.i386.rpm
```

## Installing Source Code Applications

Many programs are available for Linux in source code format. These programs are stored in a compressed archive that you need to decompress and then extract. The resulting source code can then be configured, compiled, and installed on your system. The process has been simplified to the extent that it involves not much more than installing an RPM package. The following example shows the common method to extract, compile, and install software, in this case the **kat** program, a desktop search and indexing tool. Always check the included README and INSTALL files that come with the source code to check the appropriate method for creating and installing that software.

> **TIP** *Be sure that you have installed all development packages onto your system. Development packages contain the key components such as the compiler, GNOME and KDE headers and libraries, and preprocessors. You cannot compile source code software without them.*

First you locate the software and then you download it to your system. It is downloaded in a file named **freeciv-2.0.8-7.tar.bz2**. Then decompress and extract the file either with the Archive Manager on the desktop, or with the **tar** command in a terminal window.

## Extracting the Archive

The easiest way to extract compressed archives is to use the Archive Manager (Applications | System Tools | Archive Manager) on GNOME. Either double-click the compressed archive file or right-click and select Open With “Archive Manager”. This displays the top-level contents of the archive, which you can browse if you wish, even reading text files like README and INSTALL files. You can also see what files will actually be installed. Use the Back, Forward, and Up buttons to navigate, and double-click a directory to open it. Nothing is extracted at this point. To extract the archive, click Extract.

To use the **tar** command, first open a terminal window (select Terminal in the Applications | System Tools menu). At the prompt, enter the **tar** command with the **xvjf** options (**j** for **bz2** and **z** for **gz**), as shown here:

```
tar xvjf freeciv-2.0.8-7.tar.bz2
```

## Configure, Compile, and Install

Extracting the archive will create a directory with the name of the software, in this case **freeciv-2.0.1**. Once it is extracted, you have to configure, compile, and install the software. This usually needs to be done from a terminal window.

Change to the software directory with the **cd** command:

```
cd freeciv-2.0.8-7
```

First read the INSTALL or README files included with the software and follow the instructions. Most software just uses the three following commands, but there are variations. Issue the command ./configure. This generates a compiler configuration for your particular system.

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

Most KDE- and GNOME-compliant software will also place an entry for the program in the appropriate menus—for example, a freeciv entry will be placed in the KDE Applications menu. You can then run freeciv from the menu entry. You could also open a terminal window and enter the program’s name.

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
- Integrity checks such as modification digests guarantee that messages and data have not been intercepted and changed or substituted on route.
- Authentication methods such as digital signatures can verify that the user claiming to send a message or access your system is actually that person.

## Security Services

Fedora includes several security services for protecting your system and your network transmissions (see Table 4-3). Using GNU Privacy Guard (GPG), you can encrypt your e-mail messages or files you want to send, as well as sign them with an encrypted digital signature authenticating that the message was sent by you. The digital signature also includes encrypted modification digest information that provides an integrity check, allowing the recipient to verify that the message received is the original and not one that has been changed or substituted.

With Security-Enhanced Linux a refined administrative approach is provided for greater security controls. User access to different parts of the operating system can be limited using roles and security contexts. Only qualified users can have access to certain objects like files and applications. Security-Enhanced Linux policy can be either strict or targeted. A targeted policy applies restrictions to daemons like Internet servers, restricting access for users that access those servers. You can choose which servers you want controlled. Use the system-config-securitylevel tool’s SE Linux panel to select the servers you want managed by SE Linux.

A good foundation for your network security is to set up a Linux system to operate as a firewall for your network, protecting it from unauthorized access. You can use a firewall to implement either packet filtering or proxies. *Packet filtering* is simply the process of deciding whether a packet received by the firewall host should be passed on into the local system or network. The firewall package currently in use is Netfilter (iptables). To implement a firewall, you simply provide a series of rules to govern what kind of access you want to allow on your system. If that system is also a gateway for a private network, the system’s firewall capability can effectively protect the network from outside attacks. You can provide a simple configuration for your own system using system-config-securitylevel, as well as a more complete configuration and management with system-config-selinux. Be sure to check the Fedora SE Linux FAQ at fedora.redhat.com/docs/selinux-faq for implementation details and problems on using SE Linux on Fedora.

For virus protection, you can use the ClamAV virus tools (Fedora repository). kclamav and clamtk provide desktop interfaces. Though designed for mail servers, on access and user initiated scanning is supported (clamscan and clamd). See www.clamav.net for more details.

To further control access to your system, you can provide secure user authentication with encrypted passwords, a Lightweight Directory Access Protocol (LDAP) service, and Pluggable Authentication Modules (PAM). User authentication can further be controlled for certain services by Kerberos servers. Kerberos authentication provides another level of security whereby individual services can be protected, allowing use of a service only to users who are cleared for access. LDAP and Kerberos are all enabled and configured with system-config-authentication (Authentication in the System Administration menu).

To protect remote connections from hosts outside your network, transmissions can be encrypted. For Linux systems, you can use the Secure Shell (SSH) suite of programs to encrypt any transmissions, preventing them from being read by anyone else. The SSH programs are meant to replace the remote tools such as rsh and rcp, which perform no encryption.

The IPsec protocol also provides encryption of network transmissions, but integrated into the IP packet structure. With IPsec you can both encrypt and authenticate transmissions, ensuring that they were not intercepted and tampered with, and you can implement virtual private networks (VPNs), using encrypted transmissions to connect one local network to another using a larger network like the Internet.

You can find the latest news on security issues at the Red Hat Web site (www.redhat.com) along with other Linux sites such as Linux Security (www.linuxsecurity.com), Linux Weekly News (lwn.net), and Linux Today (linxtoday.com).

> NOTE Numerous older security applications are also available for Linux such as COPS (Computer Oracle and Password System) to check password security; Tiger, which scans your system for unusual or unprotected files; and SATAN (Security Administration Tool for Analyzing Networks), which checks your system for security holes. Crack is a newer password auditing tool that you can use to check how well your password security performs under dictionary attacks.

## Authentication Configuration

To confirm that user identities are valid, your network may provide several authentication services. These can be enabled on your system using system-config-authentication (system-config-authentication). You can invoke system-config-authentication by selecting Authentication from the System Administration menu. The system-config-authentication tool consists of three panels, User Information, Authentication, and Options. Configuration consists primarily of specifying the address of the service’s server on your network. The User Information panel is used for services like NIS and LDAP, which maintain configuration information about systems

| Applications | Description |
| --- | --- |
| GNU Privacy Guard (GPG) | Encryption and digital signatures<br><b>www.gnupg.org</b> |
| Netfilter (iptables) | Firewall packet filtering<br><b>www.netfilter.org</b> |
| Security-Enhanced Linux (SELinux) | Security-Enhanced Linux<br><b>www.nsa.gov/selinux</b> |
| system-config-selinux | Fedora tool to configure and manage your SELinux policy |
| ClamAV | Virus protection with automatic update.<br><b>www.clamav.net</b> |
| OpenSSH | Secure Shell encryption and authentication for remote access<br><b>www.openssh.org</b> |
| Kerberos | User authentication for access to services<br><b>web.mit.edu/kerberos/www</b> |
| Pluggable Authorization Modules (PAM) | Authentication management and configuration |
| Shadow passwords | Password encryption |
| Lightweight Directory Access Protocol (LDAP) | User management and authorization<br><b>www.openldap.org</b> |
| system-config-authentication | Fedora tool to enable and configure authentication tools: Kerberos, LDAP, and shadow passwords |
| Internet Protocol Security (IPsec) | Protocol to implement Virtual Private Networks |

**TABLE 4-3** Security Applications
