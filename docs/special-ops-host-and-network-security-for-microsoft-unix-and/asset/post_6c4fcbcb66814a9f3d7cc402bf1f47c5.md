
Automatic updates The automatic update feature allows users to schedule and install relevant system and security updates through Web-based connections to Microsoft. Forced automatic updates for your system ensure that you have the latest versions of software are kept up-to-date with the security fixes and system patches. There is no security impact (providing that you install the system patches and hotfixes). This function is not XP-specific. 

Update Catalog The Windows Update Catalog serves as a guide for users to verify that their specific systems have the most up-to-date system fixes. It allows third parties and internal users to create applications that can utilize the catalog to ensure systems, organizations, and network remain compliant. There is no security impact from this function. It is not XP-specific.

Internet Explorer 6 Administration Kit The Internet Explorer (IE6) Administration Kit allows for an Administrator to configure media settings, security policy settings, and personalized features and to download rule sets. The feature allows network engineers and administrators increased flexibility for the deployment of IE. There is no security impact from this feature. It is not XP-specific.

Remote OS installation The remote OS installation is not unique in design, but it allows users to install Windows XP and other operating systems over the network, provided that your network has implemented an Active Directory (AD) infrastructure. The obvious benefit is that it saves time for administrators and decreases complications. There is no security impact from this feature, as long as the “Install Tunnel” is trusted. It is not XP-specific.

Windows Management Instrumentation (WMI) The WMI is one of the great features for third-party developers who desire their software to interact with the Microsoft OS. It provides an adequate API for accessing systems resources. It allows Administrators to manage system resources using internally developed or third-party applications. An excellent resource! There are numerous security concerns for this feature, all which revolve around the concept of keeping this API secure and allowing only Administrators to utilize it. It can control just about all of the Microsoft Windows platform or at least anything important. This feature is not XP-specific.

## Chapter 4 · Attacking and Defending Windows XP Professional

- Network bridge the network bridge feature allows a system to faultlessly transfer or extend communication between different types of networks. It potentially allows one system to communicate via multiple medias simultaneously. There is no security impact from this feature. It is not XP-specific (versions of this have existed in the past, yet wireless media is now incorporated).

- Internet Connection Sharing (ICS) The ICS feature is geared towards home networks and small businesses that require Internet connection services for a small amount of systems. It allows one system to act as the network relay to the Internet, thereby sharing bandwidth. ICS has built-in functions to include network address translation (NAT), system addressing, and domain name resolution services (DNS). It saves money and network resources allowing others to simply connect via the specified system. In terms of security impact, if the ICS server compromised all data going to and from the systems on the local network to the Internet would be compromised since it is routed through the ICS server. Sessions could be hijacked or redirected, DNS could be corrupted, and the network connection could be killed, to mention a few. Remember, the system is the center for communication and is trusted by the clients. This feature is not XP-specific.

- Dual processor and memory support XP Professional includes the capability to support dual processors and up to 4GB of memory. This kind of functionality was designed for computer game advocates, graphic designers, engineers, software developers, and others that require powerful processing systems. The feature allows XP Professional to be used in a more CPU/hardware-intensive environment. There is no security impact from this feature. It is XP-specific (XP Home does not have this however; other Microsoft server platforms such as NT and 2000 do have this capacity).

- Decreased system reboot frequency Due to the nature of the environment, Windows XP decreased the number of instances that require system reboots by modifying the system in real-time. The motion is similar to that of a Unix environment. It saves user time and allows for the system to stay in production mode. There is no security impact from this feature. It is XP-specific.

## Attacking and Defending Windows Professional • Chapter 4

- **Dual DLL support** The dual dynamical link library (DLL) support allows users to simultaneously run multiple versions of the same product on the system. It allows multiple versions of the same product to reside on the system, which is an excellent feature for developers and product professionals. There is no security impact from this feature (the DLLs do not execute in the memory space). It is XP-specific.

- **Offline files and directories** the feature permits a user to specify network-based files and folders, in which they have proper access, to store, modify, and resynchronize with the online versions. It allows users to modify network-based resources offline. In terms of security impact, if proper access is not controlled at the network-layer, malicious files could be synchronized upward. For instance, a macro-virus could be saved to an online document. It is XP-specific (similar, weaker versions of this existed in previous Windows 2000 releases).

- **Offline Web page viewing** Offline Web page viewing information locally for Web sites that you choose, allowing you to view the pages at a later time. It minimizes time that user must be connected to the network allowing pages or articles to be viewed at a later period of time. The security impact is that if malicious script or objects were included in the saved Web page then the storing and reloading of the Web page could adversely affect the system as if it were online. This feature is XP-specific.

- **Microsoft Management Console (MMC)** The MMC is an excellent tool that allows a user to manage system settings including users, groups, security policy settings, auditing configurations, hardware, event/system/security logs, applications, others. It is a great tool that allows manage all settings from within a single interface. There is no security impact (just understand that this is a tool is not XP-specific.

### Security Focused Features

Microsoft invested a significant amount of resources in the design and implementation of the security model for Windows XP. Multiple key features have been added that automatically harden the system. Features range from kernel modifications to software

img/729efc56f204a2ebffb8295c3a2dfdfb_119.png

## Chapter 4 · Attacking and Defending Windows Professional restriction-based access control lists. The key additions are further detailed throughout this section.

- **Kernel data structures** Microsoft has altered the protection schema for kernel data structures to the extent that all of them are read-only. Since the kernel data structures are read-only, there is minimal change for applications to disrupt them. There is no security impact, unless you have significant experience in reverse engineering assembly code used to create spinlocks. This feature is XP-specific.

- **Increased file protection** Windows XP increased the protection for core OS files from being manipulated, overwritten, or deleted during application installations. The protections that were put in place monitor the system calls for file removal, and if an error occurs, the restore function will allow you to remove the installation. It benefits the user by adding protection to files for post-installation errors. There is no security impact from this feature. It is XP-specific.

- **Software Restriction Policies** The Software Restriction Policies allow for a policy-driven mechanism to identify software that runs on the local environment. The focus behind the feature is to eliminate numerous virus and Trojan-based threads. It allows for added protection against malicious application-layer attacks through an enterprise-level mechanism. In terms of security impact, Software Restriction Policies allow administrators to configure policies to disallow the execution of certain types of files. This feature is XP-specific.

- **Encrypting File System (EFS)** EFS secures system files and folders with an internal key derived from user authentication credentials. It is simple to use, to the extent that you need to right-click on the file and select **Encrypt**. It is an easy method for securing critical files with standard cryptography algorithms. In terms of security impact, in numerous cases EFS is mistaken for a highly secure cryptography algorithm in which the user gets encryption settings. EFS does not hide files nor does it secure files in any means besides local encryption. A user would be able to brute-force the file payload if it were to be intercepted or retrieved from the local system. In addition, it might be difficult to recover EFS-encrypted files that have been moved to other systems with different users. This feature is not XP-specific.

img/729efc56f204a2ebffb8295c3a2dfdfb_120_0.png
