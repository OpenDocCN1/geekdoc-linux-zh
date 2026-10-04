
# Attacking and Defending Windows 2000 • Chapter 5

controlled adequately. The Remote Registry Service allows manipulation of the Registry from remote sources. A caution, here: You must weigh the benefits and drawbacks of this service. If you disable it, you will lose some management capability through MMC functions that modify the Registry. Microsoft introduced the RUNAS service in Windows 2000. This service allows the use of alternate credentials to perform system administrative tasks. It is a risk factor if administrative accounts and passwords are not properly configured and secured. The Server service allows sharing of resources on the network and connection via named pipes connections. The Workstation service allows network connections to remote resources.

# NOTE

Table 5.1 includes the Automatic Updates service and BITS service. These are not installed by default unless installation is based on media with Windows 2000 Service Pack 3 integrated into it. I have assumed that new installations will include slipstreamed service packs and have included those items of concern with the charts in this section. I noted that the RUNAS service is a security concern if administrative account information is not properly handled. It is, of course, a valuable tool that allows administrators to operate in their normal operations with nonadministrative credentials and change to administrator level to perform administrative tasks, which improves security, subject to the previous caveat.

# Network Services

As with the basic services that are areas of concern, there are a number of network services that are installed and available after a default installation. Table 5.2 lists the default services that are installed (it does not include services such as Domain Name Service [DNS], Dynamic Host Configuration Protocol [DHCP], WINS, and others not part of basic setup).

![](img/729efc56f204a2ebffb8295c3a2dfdfb_211_0.png)

# Table 5.2 Network Services in a Default Installation

| Network Service | W2K Professional | W2K Server |
|---|---|---|
| FTP Publishing service | No | Yes |
| IIS Admin | No | Yes |
| WWW Publishing service | No | Yes |
| TCP/IP NetBIOS Helper service | Yes | Yes |
| Telnet | No | Yes |

As mentioned earlier, IIS 5.0 is installed in a default installation of Windows 2000 server. This installation creates a Web server and FTP server, and both of these are wide open for attack if left in their default states. Additionally, this default installation is often ignored during setup while other issues are being addressed. A default installation either on a FAT partition or an NTFS 5.0 partition that has not been secured is a wide open target, and will be breached in a very short amount of time.

All platforms install the Transmission Control Protocol/ Internet Protocol (TCP/IP) Network Basic Input/Output Service (NetBIOS) Helper service to assist with NetBIOS over TCP/IP capabilities (NetBT). In Windows 2000, this service is used for NetBIOS resolution in a different manner than in former Windows versions. In later sections, I show you that this allows another point of entry and enumeration of your networks, so it is a security concern. In fact, you'll find that the default installations of Windows 2000 also allows an attacker to establish a null session connection while enumerating your network that allows the attacker to proceed with valid credentials to begin attack and compromise your system (null session in this environment means blank).

Windows NT 4.0 did not include a Telnet server, but Windows 2000 server does it, and is set for start by default. Although it is not automatically started and running, it remains a security concern, as it is in any other operating system. Windows 2000 servers also have an administrative tool management console for Routing and Remote Access installed by default, allowing configuration of the server as a Network Address Translation (NAT) gateway, a virtual network (VPN) server, network router, or Remote Access Service (RAS) server. Although not started in any configuration, improper access control settings or not controlling the membership of the Administrators group allows the configuration of this service, presenting a true possibility of breach in your systems.

# Attacking and Defending Windows 2000 • Chapter 5

# Files and Applications

As mentioned in the sidebar earlier, the default configuration in Windows 2000 is to allow Everyone full control permissions to the root directory on each partition on the machine. The effect of this setting is to allow full control to everyone (including anonymous access users through Web or FTP access), unless the underlying folders had permissions set differently and inheritance blocked. From a security standpoint, this means that the default condition on newly created folders or files in the root directory will inherit the Everyone Full control setting. Sharing permissions that were available on the Win9x platforms will be present by default File and Print Sharing is enabled, these provide only minimal security in the case of network access, and no security at all interactive access. There are, however, specific places where the default permissions change if the installation was done with the drives formatted with NTFS 5.0. A rather significant change that occurs if the installation was clean instead of an upgrade is that the Program directory permissions are significantly tightened. In this case, users may not write to the directory, which limits their ability to install applications. Additionally, a major change is made to the DACL for the HK Local Machine Registry key, where the permissions are changed to not allow users or power users to change configurations that require a write operation on the Registry. For instance, the default in a clean NTFS 5.0 Windows 2000 installation would not allow users or power users to modify network settings on their network adapters property sheet, because when these settings change they are recorded in the Registry, and this is not allowed.

> As with any installation of operating systems, it is always preferred to perform a clean install when possible. In the case of Windows 2000, an upgrade from a previous operating system will leave permissions in place that were established by the former operating system and will not include the more stringent protections afforded by the Windows 2000 operating system. Avoid upgrade installations if at all possible.

![](img/729efc56f204a2ebffb8295c3a2dfdfb_213_0.png)

# Chapter 5 · Attacking and Defending Windows 2000

# Accounts Data

Accounts data for accounts that are stored in the local machine's Security Accounts Manager (SAM) database is “secure” in the sense that the database is in and therefore locked via a file locking mechanism while the operating system is running. However, someone could boot with a faulty floppy, copy the database from its default location, and use any number of tools to attack it. Additionally, if the attacker can physically access the machine, they can simply delete the SAM database. When the machine is rebooted, the administrator account is re-created with a blank password. (Of course, all of the other accounts are removed at the same time.) This information is also retrieveable, of course, if backup media is not protected from theft or unauthorized use, because operations normally include the database information. Accounts data is vulnerable to attack when stored locally if the machines are not physically secure. A number of tools exist for searching NTFS drives and retrieving data from, which will be discussed in some of the later sections of this chapter. Remember the Ten Immutable Laws of Security by Scott Culp (www.microsoft.com/technet/review/default.asp?url=/technet/columns/security/essays/default.asp?) Law #3 says “If a bad guy has unrestricted physical access to your computer, it’s not your computer anymore.” That is absolutely the case in this instance; you must provide the basic physical security that is necessary in order to protect against this vulnerability. I discuss some ways to protect this data later in the chapter.

# Providing Basic Security Levels in Windows 2000

Microsoft provide administrators with a number of capabilities to provide basic security levels in Windows 2000. In the next sections, I discuss a number of ways to measure and check security configurations to assure that they meet the standards defined in a security baseline analysis completed to implementation. I discuss security templates, including analysis, customization, and installing and verifying their function and settings. Following that, I discuss file system and disk configuration areas to see what must be done to provide basic levels of security to users and systems. At the end of this section, I cover the configuration of services and then configuration of local and network access controls.

![](img/729efc56f204a2ebffb8295c3a2dfdfb_214_0.png)
