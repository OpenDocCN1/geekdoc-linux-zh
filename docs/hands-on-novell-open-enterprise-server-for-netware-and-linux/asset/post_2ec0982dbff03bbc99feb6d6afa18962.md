
6. A(n) ____________________ computer accesses network services, such as shared files and printers.
   - a. server
   - b. peer-to-peer
   - c. client
   - d. NOS

7. Which of the following protocols does Windows use to find a computer's address by broadcasting its name on the network?
   - a. TCP/IP
   - b. SPX
   - c. NetBIOS
   - d. IPX

8. Which of the following services works with client computers in running application software?
   - a. file service
   - b. application service
   - c. messaging service
   - d. directory service

9. Which of the following Novell services enables mobile computers to synchronize files with a central server automatically?
   - a. iFolder
   - b. iManager
   - c. iPI
   - d. NfAP

10. Which of the following is a feature of eDirectory? (Choose all that apply.)
   - a. a domain-oriented structure
   - b. specialized domain controllers
   - c. capability to run on a variety of operating systems
   - d. objects grouped into containers called Organizational Units

11. Operating system software that provides network services is referred to as the ____________________
   - a. client
   - b. NOS
   - c. daemon
   - d. DOS

12. Which of the following systems allows client computers to perform server functions?
   - a. peer-to-peer
   - b. network-centric
   - c. NOS
   - d. X.500

13. Directory services are used with peer-to-peer operating systems. True or False?

14. When using NetWare 6.5, ____________________ provides a global database of user and other network objects.
   - a. Active Directory
   - b. the NOS
   - c. the eDirectory service
   - d. NDS

15. A ______ provides rules used to communicate between computer systems on a network.
   - a. protocol
   - b. topology
   - c. NIC
   - d. media type

16. Which of the following networks consists of a fiber-optic or microwave link between buildings in the same city?
   - a. WAN
   - b. MAN
   - c. LAN
   - d. SAN

17. How would you configure a user's Windows computer to prevent him or her from having to log in to both Novell and the local computer?
   - a. Install the Novell client.
   - b. Remove the Novell client.
   - c. Create a local user name with the same password as the NetWare user name.
   - d. Remove the local user account.

18. ______ is a proprietary protocol owned by Novell.
   - a. NetBEUI
   - b. NetBIOS
   - c. IPX
   - d. TCP/IP

19. ______ application services are often part of database systems in which client computers make requests for specific data records from database services running on a server.
   - a. Server-centric
   - b. Clustering
   - c. Peer-to-peer
   - d. Client-server

20. Computers in Microsoft peer-to-peer networks are organized into logical units called ______.
   - a. forests
   - b. domains
   - c. workgroups
   - d. trees

## CASE PROJECTS

![](img/840007e8f98ea6653e5877e945c27dc6_52_0.png)

### Case Project 1-1: Designing a Network System for the Wiggerts Heating and Air-Conditioning Company

The Wiggerts Heating and Air-Conditioning Company, headquartered in Duluth, Minnesota, is a supplier and installer of heating and air-conditioning systems throughout the Midwest. In addition to supplying heating and air-conditioning equipment to dealers and stores, the company offers installation and repair services. Given the information shown in Figure 1-14, diagram the network hardware components needed to connect all computers to a centralized server with a star-based network topology.

![](img/840007e8f98ea6653e5877e945c27dc6_53_0.png)

- C = Computer
- L = Laser printer
- PS = PostScript
- PL = Plotter
- CAD = CAD computer

What other hardware components would you recommend be included on the network server?

### Case Project 1-2: Selecting a Network Operating System for the Wiggerts Heating and Air-Conditioning Company

Identify the network operating system you think would meet this organization's needs in the most economical way, and include your reasons for selecting it.

## CHAPTER 2

### INSTALLING NOVell NETWARE 6.5 OPEN ENTERPRISE SERVER

After reading this chapter and completing the activities, you will be able to:

- Identify the requirements for installing NetWare 6.5
- Perform a NetWare 6.5 Open Enterprise Server installation
- Identify and be able to use basic NetWare console commands
- Monitor server health and performance

As networks grow, installing new servers and upgrading existing servers are ongoing processes that network administrators need to perform. Although your primary responsibility as a network administrator will be setting up and maintaining the network environment, to become a CNA you also need to know how to plan for and perform a basic NetWare 6.5 installation. In addition, in this chapter you learn how to use NetWare console commands and remote management utilities to manage your NetWare 6.5 Open Enterprise Server environment.

### PREPARING FOR NetWARE 6.5 INSTALLATION

As described in Chapter 1, Novell's NetWare operating system has a long history of providing high-performance, reliable network services since the early 1980s. NetWare 6.5, the latest version of the NetWare kernel included in Novell's Open Enterprise Server distribution, continues to provide support for all Novell services and offers a wide range of development tools and utilities. Before performing a NetWare 6.5 Open Enterprise Server installation, you need to be prepared to supply information that the installation procedure requires and should be familiar with NetWare 6.5 hardware requirements and installation options. In this section, you learn the hardware requirements and the information for configuring the server and software components correctly.

#### NetWare 6.5 Hardware Requirements

Essentially, NetWare 6.5 consists of an OS kernel (Server.exe) that provides core NetWare server services to the network and a software bus that allows other modules containing specialized services and control functions to be loaded and unloaded, as shown in Figure 2-1.

![](img/840007e8f98ea6653e5877e945c27dc6_55_0.png)

**Figure 2-1** NetWare 6.5 architecture

In addition to providing basic core NetWare services and support for loadable modules, the NetWare 6.5 kernel has been designed to support Java applications and provide Internet services using HTTP. These capabilities require additional system resources, such as processor speed and memory, that weren't needed in earlier NetWare versions. Because of its modular design, the hardware requirements needed to run NetWare 6.5 vary based on the number of modules and services to be loaded and the number of users logging in. The minimum hardware environment for installing a NetWare 6.5 server is shown in Table 2-1 along with the hardware recommended to satisfactorily support an average-size network environment.

**Table 2-1** NetWare 6.5 hardware requirements

| Component | Minimum | Recommended |
| :--- | :--- | :--- |
| Processor | Pentium II or AMD K7 | Pentium IV |
| Memory | 512 MB | 1 GB |
| Disk | 500 MB DOS; 2 GB free for SYS volume | 500 MB plus 1 MB for every megabyte of RAM to allow for memory dumps (for example, 1.5 GB if you have 1 GB of RAM); 4 GB for SYS volume plus additional space for company data storage |
| Monitor | Super VGA | Super VGA |
| CD-ROM | Standard CD Drive | Bootable CD drive |

In addition to the hardware requirements, if you're installing NetWare 6.5 into an existing eDirectory tree, the eDirectory tree must be version 8.6 or later (see Chapter 4) and contain no NetWare server versions before NetWare 4.11. NetWare 6.5 also supports multiple processors to increase server performance. When using multiple processors, at least two Pentium III 700 MHz processors or later are recommended.

The NetWare 6.5 installation process consists of four major phases:

- Installation startup
- Initial installation
- Pattern selection
- Server configuration

Each phase requires entering or recording certain information. In the following sections, you prepare for the installation process by learning what information is required in each installation phase. Figure 2-2 is a sample NetWare Server Installation Planning form that you can use to help guide you through obtaining information for a successful NetWare 6.5 Open Enterprise Server installation.

### Installation Startup Phase

When the installation process starts with the **installation startup phase**, you need to select the installation language and regional settings. The regional settings include the country, code page, and keyboard. Depending on your location, you might need to change the default settings shown on the NetWare Server Installation Planning form. After accepting the NetWare 6.5 and JReport runtime license agreements, you need to select whether you want to perform a default or manual installation. For most installations, you should select the manual installation to better control the installation settings. The last step in the installation startup phase is to prepare the NetWare boot partition as described in the following section.

### NetWare Boot Partition

On a NetWare server, disk storage space is divided into two or more separate areas called partitions (see Figure 2-3).
