
providers to gather identification and authentication information all at one time during normal logon.

Winlogon is active not only during user logon and logoff but also whenever it intercepts the SAS from the keyboard. For example, when you press Ctrl+Alt+Delete while logged in, the Windows Security dialog box comes up, providing the options to log off, start the Task Manager, lock the workstation, shut down the system, and so forth. Winlogon is the process that handles this interaction.

### Local Security Authentication Server (LSASS)

The local security authentication server process (`\Winnt\System32\Lsass.exe`) receives authentication requests from Winlogon and calls the appropriate authentication package (implemented as a DLL) to perform the actual verification, such as checking whether a password matches what is stored in the active directory or the SAM (the part of the registry that contains the definition of the users and groups).

Upon a successful authentication, LSASS generates an access token object that contains the user’s security profile. Winlogon then uses this access token to create the initial shell process. Processes launched from the shell then by default inherit this access token.

### Service Control Manager (SCM)

The service control manager is a special system process running the image `.\Winnt\System32\Services.exe` that is responsible for starting, stopping, and interacting with service processes. Service processes are like Unix daemon processes in that they can be configured to start automatically at system boot time without requiring an interactive logon. Service processes run normal Win32 images that call special Win32 functions to interact with the service control manager to perform such actions as registering the service’s successful startup, responding to status requests, or pausing or shutting down the service. Services are defined in the registry under `HKLM\SYSTEM\CurrentControlSet\Services`.

To map a service process to the services contained in that process, use the `list /s` command. Note that there isn’t always one-to-one mapping between service process and running services, however, because some services share a process with other services. In the registry, the `type` code indicates whether the service runs in its own process or shares a process with other services in the image.

A number of Windows 2000 components are implemented as services, such as the spooler, event log, task scheduler, and various other networking components. To list the installed services, select Administrative Tools from the Control Panel, and then select Services.

## 4.4 Win32 API

The Win32 application programming interface is the primary programming interface to the Microsoft Windows operating system family, including Windows 2000, Windows 95, Windows 98, Windows Millennium Edition, and Windows CE. Each operating system implements a different subset of Win32. For the most part, Windows 2000 is a superset of all Win32 implementations.

Although Windows 2000 was designed to support multiple programming interfaces, Win32 is the primary, or preferred, interface to the operating system. Win32 has this position because, of the three environment subsystems (Win32, POSIX, and OS/2), it provides the greatest access to the underlying Windows 2000 system services.

The Win32 API documentation can be viewed on line at `msdn.microsoft.com`. It can also be installed by downloading the Platform SDK (available for free at `msdn.microsoft.com`). The Platform SDK contains the C header files and libraries necessary to compile and link Win32 applications. (Although Microsoft Visual C++ comes with a copy of these header files, the versions contained in the Platform SDK always match the latest version of the Windows operating systems, whereas the version that comes with Visual C++ might be an older version that was current when Visual C++ was released.)

The following is an overview of the major groups of Win32 system calls:

- **Base services**: processes and threads, memory management, synchronization, device and file I/O, error handling, debugging, event logging, interprocess communication, power management, and system configuration
- **Graphics**: functions that deal with graphical output, such as bitmaps, pens, brushes, fonts, text, and colors
- **Window management**: windows, desktops, mouse and keyboard input, buttons, cursors, dialog boxes, icons, menu, scroll bars, and other controls

Note that these represent only the core system calls—the Platform SDK describes over 100 groups of functions for building applications, such as COM+ (a framework for building n-tier distributed applications), data services, multimedia, and Web services.

## 4.5 Tools to Explore Windows 2000

Many details about the internals of Windows 2000 can be exposed and demonstrated by using a variety of available tools, such as those that come with Windows 2000, the Windows 2000 Support Tools, the Windows 2000 resource kits, and the Windows debugging tools. These tool packages are briefly introduced next.

### 4.5.1 Windows 2000 Support Tools

The Windows 2000 Support Tools consist of about forty tools useful in administering and troubleshooting Windows 2000 systems. Many of these tools were formerly part of the Windows NT 4 resource kits. You can install the Support Tools by running **Setup.exe** in the `\Support\Tools` folder on any Windows 2000 product distribution CD. (That is, the Support Tools are the same on Windows 2000 Professional, Server, and Advanced Server.)

### 4.5.2 Windows 2000 Resource Kits

The Windows 2000 resource kits supplement the Support Tools, adding some two hundred additional tools. Besides including many tools useful for displaying internal system state, they contain useful internals documentation, such as the Registry Reference and Performance Counters help files. There are two editions of the resource kits: the Windows 2000 Professional Resource Kit and the Windows 2000 Server Resource Kit. For updates to tools, as well as for new tools, see the Web site `www.reskit.com`.

### 4.5.3 Debugging Tools

The Debugging Tools for Windows package, available for download from `www.microsoft.com/ddk/debugging`, contains tools and documentation for advanced debugging and troubleshooting. For example, the package includes the Microsoft kernel debuggers, which, although used mainly for analyzing crash dumps or debugging device drivers, can also be used to investigate Windows 2000 internals because they can display internal system information not visible through any standard utility. For example, they can dump internal data structures such as thread blocks, process blocks, page tables, I/O, and pool structures. For more information, see the debugging tools help file included with this package. It explains how to set up and use the kernel debuggers (as well as other debugging and support tools that are part of the package).

### 4.5.4 Device Driver Kit

The Windows 2000 DDK is part of the MSDN Professional (and Universal) subscription, but it is also available for free download at `www.microsoft.com/ddk`. Although the DDK is aimed at device driver developers, the DDK is an abundant source of Windows 2000 internals information. For example, the DDK documentation contains a comprehensive description of the Windows 2000 I/O system in both a tutorial and reference form, including the internal system routines and data structures used by device drivers. Besides the documentation, the DDK contains header files that define key internal data structures and constants as well as interfaces to many internal system routines (in particular, Wdm.h).

### 4.5.5 Sysinternals Tools

Another source of useful troubleshooting and analysis tools is www.sysinternals.com.

## 5 Network Hardware

Thomas Sterling

Networking converts a shelf full of PCs into a single system. Networking also allows a system to be accessed remotely and to provide services to remote clients. The incredible growth of both the Internet and enterprise-specific intranets has resulted in the availability of high-performance, low-cost networking hardware that Beowulf systems use to create a single system from a collection of nodes. This chapter reviews networking hardware, with a particular emphasis on Fast Ethernet because of its superb price/performance ratio.

For Beowulf systems, the most demanding communication requirements are not with the external environment but with the other nodes on the system area network. In a Beowulf system, every Beowulf node may need to interact with every other node, independently or together, to move a wide range of data types between processors. Such data may be large blocks of contiguous information representing subpartitions of very large global data sets, small packets containing single values, or synchronization signals in support of collective operation. In the former case, a high bandwidth communication path may be required. In the latter case, low latency communication is required to expedite execution. Requirements in both cases are highly sensitive to the characteristics of the parallel program being executed. In any case, communications capability will determine the generality of the Beowulf-class system and the degree of difficulty in constructing efficient programs. The choice of network hardware and software dictates the nature of this capability.

Section 5.1 introduces some of the most popular networking technologies for Beowulf clusters. In Section 5.2, we take a detailed look at the most popular networking choice, Fast Ethernet (and Gigabit Ethernet). We conclude in Section 5.3 with comments on interconnect technology choice and some other practical issues.

### 5.1 Interconnect Technologies

In spite of its popular use in existing Beowulfs, Ethernet-based networking is not the only technology choice for enabling internode communication. Other solutions exist that can deliver equal or better performance depending on the application. Fast Ethernet is a popular choice because of its ubiquity and consequent low price. A Fast Ethernet card costs only about 2 percent of the price of today's $1,000 Beowulf nodes. Only the network switches have a significant impact on the overall price of the system. With other networking technologies, each network interface card can cost as much as a 16-port Fast Ethernet switch. So you have to think carefully before committing to an alternative network. If the kinds of applications you intend
