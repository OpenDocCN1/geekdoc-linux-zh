
## Appendix C
### Working with VMware Workstation 5

VMware Workstation 5 gives you a way to run other operating systems on your Windows XP desktop by creating virtual computer environments. You can experiment with other OSs without having to create a system or disk partition and keep copies of older OSs for use in troubleshooting or testing software applications. In this book, you can use VMware Workstation to perform activities by installing and running Windows XP, NetWare 6.5, and SUSE Linux in virtual computers on your Windows XP desktop. With virtual machines in the classroom, you can have full administrative control of your virtual system without affecting the desktop environment. In addition, using VMware Workstation enables you to suspend your system so that you can continue work later or take a snapshot of your system if you need to return to a specific point because you made a mistake. Because virtual machines can communicate with each other, using VMware Workstation allows you to simulate the lab network on your desktop. In this appendix, you learn how to install VMware, create new virtual computers, configure virtual machine settings, and start and stop virtual machines.

### Introduction to VMware Workstation

Virtual machine software works by emulating a computer’s hardware environment, including the hard drive, memory, network interface, and peripheral devices (such as modems and LPT/COM ports), as shown in Figure C-1. VMware Workstation uses disk files on the desktop computer to emulate an entire disk drive for each virtual computer. For this reason, you can use virtual machines to install multiple OSs on your desktop without creating additional disk partitions.

![](img/840007e8f98ea6653e5877e945c27dc6_617_0.png)

In addition, a section of the desktop computer’s memory is reserved for use by each virtual machine. Peripheral devices, such as network cards and USB ports, can be shared by the virtual computer and desktop OS. Certain peripherals, such as the keyboard and mouse, can be used by only one OS at a time. VMware solves this problem by allowing users to give control of the keyboard and mouse to a virtual PC.

VMware virtual machines are managed through the VMware Console, shown in Figure C-2. You can use this console to create new virtual machines, configure virtual machine settings, remove existing virtual machines, perform an OS installation, and start and stop virtual machines.

### System Requirements to Run VMware Workstation

One of the major requirements for running virtual machine software is having a large amount of RAM on your desktop. You should have a minimum of 256 MB RAM plus at least 128 MB RAM for your XP virtual machine, 256 MB RAM for a SUSE Linux server, and 512 MB RAM for NetWare 6.5. The more memory you have, the better your virtual computers will perform.

You can use VMware to perform the activities in this book in two ways. First, work in teams with each team consisting of two computers. One computer should have at least 768 MB RAM to run the virtual NetWare 6.5 server, and the other computer should have a minimum of 512 MB of RAM to run the virtual Windows XP or Linux client system. Second, work individually with a computer capable of running the NetWare 6.5 server and Windows XP computer simultaneously. This configuration requires at least 896 MB RAM (512 for the virtual NetWare 6.5 server, 128 for the virtual Windows XP client, and 256 for the desktop XP system).

![](img/840007e8f98ea6653e5877e945c27dc6_618_0.png)

### Obtaining VMware Workstation Software

There are two major virtual machine software products: VMware and Microsoft Virtual PC. Microsoft purchased Virtual PC software from the Connectix company early in 2004. Before this acquisition, VMware was the major supplier of virtual machine software. A major advantage of VMware over Microsoft Virtual PC is VMware's capability of running a variety of OSs, including Windows, Linux, and NetWare. By contrast, Virtual PC software is intended to support earlier versions of the Windows OS to make migration and testing easier. Although running non-Windows OSs on Virtual PC is possible, it's not supported and could cause intermittent problems.

VMware offers a number of software products for using virtual machine technology in a variety of environments. The following sections describe a few of the most commonly used VMware products and their features. You can find more information on this product and download the trial version and VMware Player at www.vmware.com.

### VMware Workstation 5

VMware Workstation is available in both full and Player editions. VMware Workstation and VMware Player are intended to allow software developers, testers, and students to run multiple OSs simultaneously on a single PC. The full edition is also available as a 30-day evaluation version. For the purpose of this book, you might want to download both the 30-day evaluation version and the free VMware Player. With this combination, you can perform all activities in this book without needing to purchase the full VMware edition. Some new features in VMware Workstation 5 include the following:

- The capability to take and manage snapshots of your operating system's state, which allows you to return to a saved state at any time
- A Snapshot Manager with a graphical view of all your system snapshots
- The capability to capture screens from virtual machines or create a movie consisting of multiple screen shots
- The capability to create teams consisting of two or more virtual machines interconnected across a LAN

### VMware Player

The Player edition is free, but you can’t use it to create new virtual machines, and its configuration options are more limited than VMware Workstation. For example, in VMware Player you can save the current machine state but you can’t take snapshots. You learn more about setting up and using VMware Player in “Using VMware Player” later in this appendix.

### VMware ESX Server

VMware ESX Server is a high-performance version of VMware Workstation that uses its own drivers to access the disk system directly, which increases access speed. It runs under Windows 2000 Server or Windows Server 2003 to provide a more powerful platform. VMware ESX Server is intended for use in data centers to implement multiple servers on a single high-performance computer system. Using ESX Server to run network operating systems, such as NetWare, Linux, or Windows, offers the following advantages over running these operating systems without VMware:

- ESX Server can increase utilization of costly computer hardware by running multiple server OSs on the same computer.
- A data center can dedicate servers to specific functions, such as DNS/DHCP servers, Web servers, database servers, and file servers, without the expense of buying additional computer systems.
- A data center can move a virtual server to another physical computer quickly and easily by simply copying the virtual machine files to the other system’s hard drive.
- Because VMware isolates the virtual server from the physical hardware of the computer system it’s running on, disaster recovery is simplified because you can restore a virtual computer’s backup to another computer without having to reinstall the OS or change the hardware configuration.

### VMware GSX Server

VMware GSX Server is similar to ESX Server except that it comes with its own kernel and doesn’t require a host OS, such as Windows XP or Windows Server 2003. Using its own kernel gives GSX Server better performance and reliability when running servers in large data centers.

## Creating New Virtual Machines

After installing VMware Workstation 5, your first task is creating a virtual machine environment for each OS version you want to install. Because the VMware Workstation 5 Player software can’t be used to create new virtual machines, you need preconfigured virtual machine files from your instructor, or you must create the files on another machine running the full edition (or a 30-day evaluation version) of VMware Workstation 5. If you’re using preconfigured files from another computer, skip to the “Add an Existing Virtual Machine” section. If not, follow the procedure in the “Create a New Virtual Machine” section to learn how to use the full or 30-day version of VMware Workstation 5 to create new virtual machines for installing Windows XP, NetWare 6.5, and SUSE Linux. No matter which version of VMware Workstation 5 you’re using, you should create a folder on the C: drive of your Windows XP computer to store virtual machines. For example, use Windows Explorer to create a folder named VMS on your C: drive. You can then place all your virtual machines in subfolders under this folder.

### Create a Virtual Machine

To install a new OS, first you need to create a virtual computer environment that defines settings such as the OS version, the location of the disk file, and the amount of RAM. Use the following steps as a guideline for creating new virtual machines for use in this book’s activities:

1. Start VMware Workstation by double-clicking the desktop icon to display the VMware Console shown previously in Figure C-2.

![](img/840007e8f98ea6653e5877e945c27dc6_619_0.png)
