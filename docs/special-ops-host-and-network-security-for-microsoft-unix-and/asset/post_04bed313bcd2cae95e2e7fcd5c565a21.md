
## Attacking and Defending Windows XP Professional · Chapter 4

Internet Information Services, domain controllers, and DNS servers have therefore summarized in comparison; the intent here is to describe the security and technology ramifications in the Windows XP Professional implementations.

## Attacking Terminal Services

Over the past year there have been numerous vulnerabilities released pertaining to Microsoft's Terminal and Terminal Services. Microsoft's Terminal Services provides terminal functionality of a system to another remote system through the use of the Remote Desktop Protocol. Numerous enhancements have been made to the Terminal Services client application and the underlying RDP backbone, yet vulnerabilities are still identified and released. Multiple security issues have been found in the form of server-side information leakage, session hijacking, client profiling, transmission data leakage, unauthenticated code execution, and denial of service attacks. Information and details on attacking defending Microsoft Terminal Server can be found in Chapter 9. You can find more information on Terminal Services at www.microsoft.com/windows2000/server/evaluation/features/terminal.asp.

## Attacking MSSQL and Oracle

Databases and database technology have always been some of the most sought out targets for malicious and curious users for the simple reason that databases contain information that could include system and network authentication credentials, personal information, documents, Web site files, images, and just about everything else. XP Professional does not come with any generic database for the user; however, it is not uncommon decision for such a database to reside on a developer or public access system. The database application resides at the application-layer of XP Professional and in most cases can be accessed locally and remotely. XP allows databases to be installed and configured in the same manner as most other applications. Pertinent database information is stored in the file system in the Registry. As you possibly know, there are many different types of attacks that can leverage sensitive information or disrupt operation. See Chapter 12 and Chapter 13 for more information on attacking and defending database technology.

## Attacking Internet Information Services

Internet Information Services (IIS) is the most popular Web server in the world, just behind the freeware Apache server. Coincidentally as it may be,

![](img/729efc56f204a2ebffb8295c3a2dfdfb_149_0.png)

# 16 Chapter 4 · Attacking and Defending Windows XP Professional

according to the statistics from the SecurityFocus vulnerability database, it has proved the most vulnerable Web server. IIS is not bundled with XP Professional by default, the back-end system allows for IIS installation after you have completed installing the OS. In terms of client-server programming, IIS is a server that publishes files to client applications that speak the same protocol, HTTP(S) over TCP/IP. Refer to Chapter 10 for detailed Web server and IIS attack techniques and general information. See http://www.microsoft.com/WindowsXP/pro/evaluation/overviews/iis.as for information on installing IIS 5.1 on XP Professional.

## Attacking Domain Controllers

Microsoft Windows utilizes a centralized authentication technology designed for enterprise organizations to aid in the problem of enterprise security, network, and policy management. The authentication server that you request network access are referred to as the domain controllers (DCs), previously known as primary domain controllers (PDCs) in Windows NT. DCs have been excellent targets for malicious users and attacks since they authenticate credentials. Some large organizations or networks could potentially have thousands to thousands of stored usernames and passwords, which would be considered a hacker's dream box. The domain controllers are comprised of Windows systems installed with the DC service, which accepts inbound authentication requests. See Chapter 5 and Chapter 6 for more information on attacking domain controllers.

## Attacking DNS Servers

The Domain Name Service (DNS) is a popular protocol, and in the case that a system is using the protocol's server functionality, it is often categorized as an easily accessible service susceptible to multiple types of attacks. Most organizations today have implemented network-based firewalls and filters to secure the network from potentially malicious and unsolicited traffic. However, in the case of DNS, most networks allow inbound DNS traffic on port 53. Therefore, most hackers have an entry point to your network or DMZ through the DNS server. Microsoft has implemented a version of DNS to... See Chapter 8 for more information on attacking and defending DNS.

![](img/729efc56f204a2ebffb8295c3a2dfdfb_150_0.png)

## Defending XP Professional

Windows XP Professional provides multiple tools, features, and functions within the core operating system that enable users and administrators to secure the infrastructure and individual systems for all layers of the communication stream. Throughout this section of the chapter, I cover specific recommendations for “locking down” or securing your Windows XP Professional system. Microsoft made noteworthy efforts to have a workstation platform that would be secured upon default installation. The time to remotely profile a system in most cases is less than 10 minutes, and it takes a much higher investment of to secure the system.

## WARNING

Microsoft Windows XP Professional is not secure via the default installation!

The XP Professional platform was designed to be the workstation operating system of choice for client systems in the business world. The flexibility and bundled features allow it to morph from a system configured specifically for a traveling user to that of a software developer who requires the beef of a dual processor. Since operating systems can be configured for multiple purposes, it is important to note that the recommendations I provide in this section are designed for an average business professional working in an environment that requires occasional travel. It is also assumed that the system will reside on a laptop in a single processor environment with some sort of sensitive data that should not be accessed by individuals. Other specific assumptions that must be made in accordance with the hardening recommendations will be noted with the security recommendation.

If properly take the steps and configuration recommendations provided here, you should have a system locked down to the best extent by the options provided by Microsoft. It is not meant to be a guide for all XP Professional systems, yet it is meant to provide additional information to administrators who want to utilize multiple features within the XP. The key areas that I focus on throughout the section can be categorized into three main concentrations: applications, system configuration, and system policies. Using an array of applications to secure your local system currently prove to

# Chapter 4 · Attacking and Defending Windows XP Professional

be a tedious task, but if Windows evolution remains the same, it is likely that some of those applications will be eventually incorporated into the core operating system. The pertinent external application is anti-virus, and configuring your system may prove to be the most cumbersome. Configuring your system policies, however, is somewhat minor in comparison to configuring your system, which in general is not an easy task, because it reviewing Software Restriction Policies, verifying your local security policy, and defining your IP security policies. Lastly, and definitely the most important task in securing your system, is configuring particulars of your system. The particulars that I referencing NT File System (NTFS) usage, securing your system and file permissions, enabling implementing an auto-update process, installing hotfixes and patches, and securing user and group permissions. Each of these concentrations will be covered in detail throughout the following section.

### Verifying NTFS Usage

The NTFS file system architecture provides multiple security and optimization advantages over other file systems you could select to install your XP Professional simply because if it is not NTFS, you may want to completely reinstall your system on a NTFS file system. NTFS has inherent protections that increase the complexity of accessing files within the OS without running in an authenticated session. It also aids in protecting files from other users accessing files to which they do not have the proper permissions. To verify if all of your disks are using NTFS, open the My Computer from the Start menu. Then right-click on each of the local disks underneath the Hard Disks heading at the top of the window. Scroll down and select Properties to ensure that it says NTFS next to File system, as shown in Figure 4.9.

> It is assumed that you do not have a dual-boot system or will not install virtual machines running with a Linux or Unix operating system. Such OSs cannot freely read data from a NTFS file system. If you require the ability to access the file system or import it into a *nix structure, you probably want your XP Professional system to reside on a FAT32 system.

www.synergy.com
