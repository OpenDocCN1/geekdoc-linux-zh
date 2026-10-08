
![](img/75f39fc91296b889c0653851accdfd46_1202_0.png)

Figure 15-8 CDE program Workspace

The program workspace is the first of the four workspaces shown on the bottom middle of Figure 15-8. There are three other workspaces for this user that we will view labeled sam, files, and icon.

Figure 15-9 shows the sam workspace in which we have invoked the System Administration Manager.

![](img/75f39fc91296b889c0653851accdfd46_1203_0.png)

Figure 15-9 CDE sam Workspace

Figure 15-10 shows the *files* workspace in which we have invoked the File Manager from CDE.

![](img/75f39fc91296b889c0653851accdfd46_1204_0.png)

Figure 15-10 CDE files Workspace

Figure 15-11 shows the icon workspace in which we have invoked the icon editor.

![](img/75f39fc91296b889c0653851accdfd46_1205_0.png)

Figure 15-11 CDE icon Workspace

This technique, using X Windows on the Windows system to display applications running on the UNIX system, is powerful in this heterogeneous environment. It is also inexpensive and simple to install. You have a choice using Exceed to either open individual UNIX windows while working on your Windows system or run the entire Common Desktop Environment from your Windows system. I find that users who spend a majority of their time working on the UNIX system, such as UNIX developers, like to run the entire Common Desktop Environment on their Windows system. Users who spend a majority of time on their Windows systems and need only occasional access to UNIX usually open a **dterm** or **xterm** window from the Windows system. Exceed gives you the flexibility to access UNIX from Windows using either technique.

We can also take this interoperability one step further by introducing data sharing into this mixed environment. Just as X Windows on UNIX and the Windows user interface are not compatible, the ways in which data is shared in UNIX and Windows environments are different. Chapter 16 covers a way in which data sharing between UNIX and Windows takes place.

## CHAPTER 16

### Networking

### Why Cover Interoperability?

Although system administration topics are pretty much the same going from operating system to operating system, the peculiarities of each operating system define how you perform a given function. For this reason, system administration is seldom covered as a general topic; rather, it is covered for a particular operating system. In this book, however, the assumption is that you have both Windows and UNIX in your environment. You need to manage both and manage them separately for the most part; however, advantages to implementing technology exist that can enhance interoperability between the two operating systems.

What I cover in the interoperability chapters of this book (Chapters 15 through 20) are some of the most basic, and at the same time some of the most useful, technologies you can put in place to help with interoperability between Windows and UNIX.

You could certainly go beyond the interoperability topics I cover to much more advanced functionality; however, what I cover in the interoperability chapters is a big interoperability gain for very little cost and effort.

This chapter and Chapter 15 combine to provide background of some useful interoperability. In this chapter, I use a networking product on the Windows system that provides transparent access to the data on the UNIX system using Network File System (NFS). In Chapter 15, I covered Windows and UNIX interoperability by running an X server program on a Windows system, providing graphical access to a UNIX system. Using the X Window System (X Windows), you have a graphical means of connecting a Windows system to a UNIX system, and using NFS, you have a way of easily sharing data between these two systems. These two technologies, X Windows and NFS, provide the foundation for a variety of other useful interoperability between the two operating systems.

Although I provide TCP/IP background earlier in the book, I am going to include it again here so that you don’t have to flip back and forth if you have to review TCP/IP.

### TCP/IP Networking Background

You can see the seven layers of network functionality in the ISO/OSI model shown in Figure 16-1. I’ll cover these layers at a cursory level, so that you have some background on this networking model. The top layers are the ones that you spend time working with, because they are closest to the functionality to which you can relate. The bottom layers are, however, also important to understand at some level, so that you can perform any configuration necessary to improve the network performance of your system and have a major impact on the overall performance of your system.

| Layer Number | Layer Name | Data Form | Comments |
| :--- | :--- | :--- | :--- |
| 7 | Application | | User applications here. |
| 6 | Presentation | | Applications prepared. |
| 5 | Session | | Applications prepared. |
| 4 | Transport | Packet | Port-to-port transportation handled by TCP. |
| 3 | Network | Datagram | Internet Protocol (IP) handles routing by going directly to the destination or default router. |
| 2 | Link | Frame | Data encapsulated in Ethernet or IEEE 802.3 with source and destination addresses. |
| 1 | Physical | | Physical connection between systems. Usually thinnet or twisted pair. |

Figure 16-1 ISO/OSI Network Layer Functions

I'll start reviewing Figure 16-1 at the bottom, with layer 1, and describe each of the four bottom layers. This model is the International Standards Organization Open Systems Interconnection (ISO/OSI) model. It is helpful to visualize the way in which networking layers interact.

### Physical Layer

The beginning is the physical interconnect between the systems on your network. Without the **physical layer**, you can't communicate between systems, and all the great functionality you would like to implement will not be possible. The physical layer converts the data you would like to transmit to the analog signals that travel along the wire (I'll assume for now that whatever physical layer you have in place uses wires). The information traveling into a network interface is taken off the wire and prepared for use by the next layer.

### Link Layer

In order to connect to other systems local to your system, you use the link layer that is able to establish a connection to all the other systems on your local segment. This is the layer where you have either IEEE 802.3 or Ethernet. These are "encapsulation" methods, named so because your data is put in one of these two forms (either IEEE 802.3 or Ethernet). Data is transferred at the link layer in frames (just another name for data), with the source and destination addresses and some other information attached. You might think that because there are two different encapsulation methods they must be much different. This conclusion, however, is not the case. IEEE 802.3 and Ethernet are nearly identical. So with the bottom two layers, you have a physical connection between your systems and data that is encapsulated into one of two formats with a source and destination address attached. Figure 16-2 lists the components of an Ethernet encapsulation and includes comments about IEEE 802.3 encapsulation where appropriate.

| Component | Size | Notes |
| :--- | :--- | :--- |
| destination address | 6 bytes | address to which data is sent |
| source address | 6 bytes | address from which data is sent |
| type | 2 bytes | the "length count" in 802.3 |
| data | 46-1500 bytes | 38-1492 bytes for 802.3 |
| crc | 4 bytes | checksum to detect errors |

**Figure 16-2 Ethernet Encapsulation**

One interesting item to note is the difference in the maximum data size between IEEE 802.3 and Ethernet of 1492 and 1500 bytes, respectively. This is the Maximum Transfer Unit (MTU). The data in
