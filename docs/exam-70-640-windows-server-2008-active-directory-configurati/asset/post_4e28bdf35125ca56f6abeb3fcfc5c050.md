
## Introducing Active Directory Domain Services

![](img/a8ee53dbf1310726255b6fbb9f296fb2_43_0.png)

The Active Directory Domain Services (AD DS) service in Windows Server 2008 provides a centralized authentication service for Microsoft networks. Some of the benefits of Active Directory DS include a hierarchical organizational structure, multi-master authentication (the ability to access and modify AD DS from multiple points of administration) to create fault tolerance and redundancy, a single point of access to network resources, and the ability to create trust relationships with external networks running previous versions of Active Directory and even UNIX. Windows Server 2008 includes a number of new features to improve Active Directory, including the introduction of the Read-Only Domain Controller (RODC), fine-grained password policies, an improved graphical user interface (GUI), improved auditing of Active Directory modification and deletions, the ability to start and stop Active Directory as a service without needing to completely restart the domain controller for maintenance, and the introduction of Server Core, a minimal installation of Windows Server 2008 that has a greatly reduced attack footprint relative to a full install of the server operating system.

## Identifying Active Directory's Functions and Benefits

Microsoft introduced the Active Directory service in Windows Server 2000 to provide the main repository for information about network users, computers, services, and other resources on a Microsoft network. Although subsequent versions of Active Directory in Windows Server 2003 and Windows Server 2008 have introduced new functionality and security features, the basic premise of the service remains the same: to provide a centralized authentication and authorization repository for large and small organizations alike.

A directory service allows businesses to define, manage, access, and secure network resources, including files, printers, people, and applications. Without the efficiency of a directory service, businesses would have difficulty keeping up with demands for fast-paced data exchange. As corporate networks continue to grow in complexity and importance, businesses require more and more from the networks that facilitate this automation. In Windows Server 2008, Microsoft provides two separate roles that can provide directory services:

- **Active Directory Domain Services (AD DS)** provides the full-fledged directory service that was referred to as *Active Directory* in Windows Server 2003 and Windows 2000.
- **Active Directory Lightweight Directory Services (AD LDS)** provides a lightweight, flexible directory platform that can be used by Active Directory developers without incurring the overhead of the full-fledged Active Directory DS directory service. For example, an application developer might use AD LDS to provide a directory of employee photographs that integrate with AD DS, without actually needing to store hundreds or thousands of graphics files throughout the company.

A Windows Server 2008 computer that has been configured with the Active Directory DS role is referred to as a *domain controller (DC)*. A domain controller is a server that stores the Active Directory database and authenticates users with the network during logon. Each domain controller actively participates in storing, modifying, and maintaining the Active Directory database information that is stored on each domain controller in a file called ntds.dit. Active Directory is a *multi-master database*, which means that administrators can update the ntds.dit from any domain controller. The process of keeping each domain controller in sync with changes that have been made elsewhere on the network is called *replication*. When a domain controller transmits replication information to other domain controllers on the network, this is called *outbound replication*. Conversely, when a domain controller receives updates to the Active Directory database from other domain controllers on the network, this is called *inbound replication*.

![](img/a8ee53dbf1310726255b6fbb9f296fb2_43_1.png)

For more information about Active Directory Lightweight Directory Services, refer to Lesson 2.

Consider a small network with three domain controllers: DC1, DC2, and DC3. A user changes her password, updating the ntds.dit database on DC1. DC1 must replicate this change to DC2 and DC3. Domain controllers automatically replicate with other domain controllers in the same domain to ensure that the Active Directory database is consistent. Windows Server 2008 relies on one or more domain controllers to manage access to network services.

Active Directory is designed to enable scalability by handling organizations of any size, from small businesses to global enterprises. In fact, Active Directory is theoretically scalable to holding 4,294,967,041 ($2^{32}$ - 255) separate objects. From a practical standpoint, this means that the maximum size of an Active Directory database is really only limited by the processing power of the hardware that has been deployed onto the domain controllers.

The major benefits of the high-powered Active Directory Domain Services include:

- Centralized resource and security administration
- Single logon for access to global resources
- Fault tolerance and redundancy
- Simplified resource location

### Centralizing Resource and Security Administration

Active Directory provides a single point from which administrators can manage network resources and their associated security objects. An organization can administer Active Directory based on an organizational model, a business model, or the types of functions being administered. For example, an organization could choose to administer Active Directory by logically dividing the users according to the departments in which they work, their geographical location, or a combination of these characteristics.

> See "Using Forest and Domain Functional Levels" later in this lesson for information on functional levels.

Active Directory can simplify the security management of all network resources and extend interoperability with a wide range of applications and devices. Management is simplified through centralized access to the administrative tools and to the Active Directory database of network resources. Interoperability with prior versions of Microsoft Windows is available in Windows Server 2008 through the use of functional levels.

When Active Directory is installed and configured, it includes a number of GUI and command-line tools that can be used to administer network services, resources, and security at a detailed level. These administrative tools can be accessed from any domain controller in the network or an administrative workstation that has these tools installed. When you configure a Windows 2008 Server as an Active Directory domain controller, you will see the following tools added to the Administrative Tools folder:

- Active Directory Users and Computers
- Active Directory Domains and Trusts
- Active Directory Sites and Services
- ADSI Edit

You will see these administrative tools described throughout this book. As you are introduced to new concepts, the tools that should be used with each associated task will be noted. This will allow you to build your administrative knowledge at a manageable pace.

> Unlike Active Directory in Windows 2000 and Windows Server 2003, Windows Server 2008 no longer supports the use of Windows NT domain controllers.

### Providing a Single Point of Access to Resources

Prior to the introduction of directory services to corporate networks, all users were required to log on to many different servers in order to access a variety of different resources. This required users to enter their authentication information multiple times, and an administrator had to maintain duplicate user accounts on every server in the organization. Imagine...
