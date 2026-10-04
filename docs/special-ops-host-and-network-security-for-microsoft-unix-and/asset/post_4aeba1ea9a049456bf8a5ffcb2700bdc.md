
# Attacking and Defending Windows 2000 • Chapter 5

## Disk Configurations

2000 introduces a new capability in disk configuration that was not available in previous versions of Windows-based operating systems. The capability is in the configuration and use of what Microsoft calls dynamic disks. Administrators and technicians are familiar with the normal DOS-type partition structure, in which the capability to establish up to four partitions per disk was the norm, and was possible to make a partition active so that it could boot an operating system. In a default Windows 2000 configuration, this is still the method that is used for disk configuration, and is called a basic disk. However, the administrator has the opportunity to change the dynamic disk configuration at any time (Don't do this if you are dual-booting with other operating system—other operating systems do not recognize the dynamic disk structure, and you won't be able to access the disk). Dynamic disks allow the administrator to utilize the full capabilities of NTFS 5.0. With dynamic disks configured, it provides the ability to create mirrored volumes, spanned volumes, and mount points in Windows 2000. The process is one way. If you want to change back to basic disks, you must back up the data, remove the partition, and re-create the disk as a basic disk. The process for conversion and much more information is available in the Windows 2000 help files.

# NOTE

> From a security standpoint, the dynamic disk configuration is superior to basic disk configuration, because a DOS/Windows boot floppy will not allow local access to the information on the drives.

## Evaluating and Configuring System Services

Common security practices require systems to be evaluated to determine what services are needed for a particular environment. When working with Windows 2000, a number of services installed by default may not be needed for a particular operation. For instance, it makes little sense to leave Internet Information Services installed on a machine that is used solely as a file server. Uninstalling IIS 5.0 and ensuring that the services related to it are removed makes the machine a more secure platform. To view and evaluate the services that are running on various machines, the administrator would use either the Services management console in Administrative Tools or access the same information from the Computer management console.

![](img/729efc56f204a2ebffb8295c3a2dfdfb_227_0.png)

# Chapter 5 · Attacking and Defending Windows 2000

In the section “Windows 2000 Basics,” I indicated some services that are a cause for concern in most environments. The capability to disable unnecessary management consoles is available, and individual machines need to be evaluated as to the needs of installed services. From the Services console, disabling unnecessary services is a simple process, as shown in Figure 5.21.

Figure 5.21 Disabling the Telnet Service

![](img/729efc56f204a2ebffb8295c3a2dfdfb_228_0.png)

At this point, simply click Apply, and the service is disabled. A manual start capability left configured the service to be started on demand, whereas the Disabled setting stops this capability.

# NOTE

Services configurations that are to be applied to systems (and should) be handled through settings in the Security Templates that were discussed earlier in the chapter. You can use the Services applet, if necessary, but it is more effective to include these configurations in the security templates you apply.

## Fine Tuning Access Control

Among many benefits of the development and introduction of Windows 2000, the ability to more precisely control access to systems and resources is the most important. Particularly in the case of machines and users configured to participate in the Active Directory domain structure, administrators and security professionals now have many of the tools that have been needed to enforce the concept of least privilege for the configuration of DACL levels and the administration of access control mechanisms.

If Windows 2000 is utilized in a workgroup environment or is not attached to a domain structure that utilizes the enhanced authentication methods (either a Windows 2000 domain or a Kerberos realm), it will utilize the NT LAN Manager (NTLM) or NTLM v2 processes for authentication and access control. These processes will be used in communication scenarios involving down level Windows clients. Given the choice, it is preferred to join machines to a Windows 2000 domain, in order to fully utilize the capabilities of the Kerberos authentication process. This provides a mid level control over access levels, the ability to delegate permission to perform various system tasks, and the use of the time-based Kerberos access token process to limit the effects of playback in your network areas.

## Defining Network Access

Windows 2000 also allows a capability to define more fully than previous operating systems who has access from the network and how they may access the resources that the administrator is charged with protecting. This expanded capability provides the ability to block or filter protocols at the individual machine level and to configure settings for IP Security security templates, as discussed previously. For instance, Windows 2000 allows the administrator during configuration of accounts and services to require specific levels of authentication, secure communication channels, and also requirements for use of IPSec and IPS policies on individual machines. Additionally, you can use the capability to allow or deny TCP and UDP ports as desired on individual machines to further protect them.

You can also control network access to resources with a combination of NTFS and share permission settings on the DACLs for folders on NTFS partitions. In the case of Windows 2000, you can map resources below the shared folder if you have been granted permission to access them. This capability was not available in Windows NT 4.0.

![](img/729efc56f204a2ebffb8295c3a2dfdfb_229_0.png)

Although much of the network security filtering necessarily occurs at the perimeter rather than the individual machine, you should consider the need for NetBIOS services and communication. In most scenarios, it is appropriate to take the necessary steps to stop NetBIOS communication on the network. I detail the steps to accomplish this task in the “Defending and Hardening Windows” section later in this chapter.

## Defining Local Access

Local access is controlled through the use of the logon process, which acts much like the NT 4.0 logon process for authentication when the machine is made a member of an Active Directory domain. At that time, access is granted through the Kerberos process, which grants tickets and creates access tokens based on group memberships. In either case, access to local resources is limited to resources for which the user has been granted access through the DACL if the drives utilize NTFS 5.0 formatting. In the case of FAT formatted drives, no local restrictions or security can be enforced with the exception of requirements for a logon process. Access cannot be controlled on local resources after logon without using NTFS.

## Attacking Windows 2000

Windows 2000 has had large number of attacks against it since its inception. In this section, I show you some of the various methods that attackers use to discover and try to access Windows 2000 equipment and domains. I discuss methods that many attackers use to check systems for vulnerabilities and then discuss methods to make these attacks profitable for the attackers and at the same time make your system more secure. I also show a pattern that has become pretty standard for detection of vulnerabilities. That standard takes a course proceeds through a multistep process to identification and attack:

+   * Footprint potential victim systems.
+   Scan for entry points.
+   Enumerate possible entry points.
+   Get passwords.
+   * Attack.
