
# 362 EMULATORS UNDER LINUX

![](img/ad3b0471a5d608a011338d028bec5422_381_0.png)

Figure 12.1 Network scheme for TCP/IP in the DOS emulator.

```
ifconfig dsn0 192.xxx.xxx.1 broadcast 192.xxx.xxx.255 \
netmask 255.255.255.0
route add -net 192.xxx.xxx.0 dsn0
```

**Listing 12.2** Configuration of the virtual network interface.

The emulator uses this interface only if the files libpacket.c and pktnew.c have been replaced with the files libpacket.c.multi and pktnew.c.multi in the ./net directory. These modules assign each tty a Virtual Ethernet address which can, for example, be used for the assignment of an Internet address via bootp. This assignment may cause problems if several emulators were started from the same window, for example under X. The Virtual Ethernet address consists of one fixed and one variable part. The address has the form 64:62:variable:78:78:78; the variable is calculated following Table 12.3 on the basis of the tty from which the emulator was started.

| tty | Third address field |
|||---|
| ttyn | n |
| ttypn | 0xC0 + n |
| ttySn | 0x40 + n |

**Table 12.3** Virtual Ethernet addresses.

# THE BIOS EMULATOR DOSemu 363

If you want to use the emulator to access not only resources in your own computer, you must also adapt the routing tables on the other computer. You can enter a static route to your computer for the virtual network assigned to the emulators.

```
route add -net 192.xxx.xxx.0 gw aaa.bbb.ccc.ddd
```

In the emulator, you can then use the standard programs that build on a packet driver, for example a multiplexer such as PKTMUX, or SOSS or XFS.

DOSemu in an IPX network DOSemu can employ two ways of gaining access to a Novell network with IPX protocol. Novell uses three different frame types (Ethernet_II, Ethernet_802.2, Ethernet_802.3). The application areas and the possibilities of integrating LINUX computers are different, so you should contact your network administrator.

- Ethernet_II is used by Novell if the server supports the IPX protocol. The IPX protocol too can make the connection of a LINUX computer relatively easily.

- The frame type Ethernet_802.3 was used by Novell before the VLM system or NetWare 4.x were introduced. With this frame, no IP packets are carried.

- Today, Novell recommends the use of Ethernet_802.2, which is also the standard for newly created servers or networks. This frame type is not supported by the DOSemu packet driver, you must either establish another frame type in the network or use IPX Linux.

The configuration of LINUX IPX requires only a few paths and has proved successful in practice through a significantly higher support and the support of all frame types. To begin with, the kernel must support the IPX protocol. If no appropriate message is displayed at the start-up of LINUX, you must configure and recompile the kernel. The prompt for 'IPX protocol' must be answered with 'y'. You also need the programs that can be found in the /ipxtutils directory in the sources of the emulator. With the ipx_interface program, you can activate the IPX protocol on your network card.

```
ipx_interface -p eth0 802.2
```

In the above example, you need to replace the device and the frame type with the device you are using or with the corresponding frame type (802.2, 802.3, or EtherII). As a last step, you need to enter the line ipxsupport in the file dosemu.conf. This concludes the configuration on the LINUX side. After you have started the emulator, you only need to start the NetWare shell NETX.EXE or VLM.EXE. You do not need LSL, IPXODI, or any other program.

# 364 EMULATORS UNDER LINUX

The second way to make a connection to an IPX network is via the virtual packet driver of the emulator. This requires no kernel support (except for the general TCP/IP). In the emulator, you must then start the following Novell programs:

- LSL
- PDETHER
- IPXODI
- VLM # or NETX

The PDETHER program is an ODI driver which builds on a packet driver. This makes it possible to transmit IPX packets via the internal packet driver of the DOS emulator. This method only functions for the frame types Ethernet II and 802.3; for the latter, the line pktdriver_hack must be activated in the configuration. If you use an ODI driver, the file NET.CFG must be adapted accordingly.

DoSEmu in other networks The DOS emulator does not provide any special support for access to other networks. Nevertheless, it may be possible to access these networks by adding another network card to the computer and loading the DOS driver into the emulator. Such cards usually make use of interrupts for controlling the card and a RAM window for communication.

The DOS emulator can process hardware interrupts if the LINUX kernel forwards them to user processes. For this, you must load the 'silly interrupt generator' kernel module. Subsequently, the corresponding interrupt can be permitted in the DoSEmu configuration by activating the line silly interrupt.

Access to the real memory of the computer can then be mapped into DOS memory by means of the keyword hardware_ram. You can find commented examples for these settings in the sample configuration.

## 12.1.5 Further developments

Inspired by the great success of LINUX as a free operating system and the need for a freely available DOS, a group was formed to work on the so-called FreeDOS project. This is intended to provide a free DOS which will still be maintained even after Microsoft and IBM have discontinued active development of DOS. First programs and the operating system itself are already available.

# THE WINDOWS EMULATOR Wine 365

| Additional Information and Sources |
|---|---|
| WWW server: | www.freedos.org |

## 12.2 The Windows emulator Wine

The Windows emulator Wine (Wine Is Not an Emulator, or Windows Emulator) converts calls of the MS Windows4 API (Application Programming Interface) into equivalent X calls. This allows Windows programs to run under X.

The development of Windows emulator Wine began when Sun announced the release of their Windows emulator Wabi. Some experienced LINUX programmers immediately began the development of the emulator, and the first versions of Wine were ported to the freely available *BSD systems. The first and most important application that ran under Wine was the Solitaire game from Windows 3.1.

This emulator is supposed to be a complete Windows emulator. Currently, it still makes use of several DLLs (Dynamic Link Libraries) from the Windows environment. Besides the compatibility with Windows 3.1, the Win32 interface is implemented as well; thus, programs for Windows-95 and Windows NT can also be run under Wine. A further goal is the development of a library (libwine) with which Windows programs can be easily ported to UNIX and X. Corel Office Suite.

However, the Wine program is not a complete Windows emulator. The authors are implementing all APIs step by step, including the Win32 API. Wine is one step ahead of the commercial Wabi which can only handle 16-bit programs. As long as not all DLLs have been implemented completely and without errors, you can require loading of the original DLL via a command line. An important milestone is running the MS Office suite. Currently, not all Windows programs are running, but the developers are working on it. A patch is released every couple of weeks, which is evidence of the progress of this development.

# 366 EMULATORS UNDER LINUX

### 12.2.1 Compilation and installation

Wine does not exist as a binary distribution. Therefore you must have the compiler installed to compile the source code. The installation of Wine also requires the X Window system to be installed together with the associated libraries and include files. An additional precondition is the libXpm library which is used for handling of bitmaps. The installation of Wine is as simple as that of the GNU programs and is limited to the use of ./configure and make.

### 12.2.2 Configuration of the emulator

Prior to its first start, the emulators need to be appropriately configured. The default, the file /usr/local/etc/wine.conf is used. Individual users can configure the emulator according to their own requirements using the file ~/.werc. Both files have exactly the same structure. You will also find a sample configuration with the name wine.ini in the Wine directory.

An important issue for starting your first programs is the assignment of drive letters to LINUX directories, and the search path for programs and DLLs. For this purpose the file wine.conf, whose syntax recalls that of the .ini files of Windows, contains various sections:

- The assignment of drive letters to the file system or devices such as disk drives is carried out in one Drive section per drive. You can specify both devices and directories of the LINUX directory tree.

```
[Drive C]
Path=/home/dos
Type=hd
Label=DOS-DISK
```

- The search paths for programs, DLLs and other paths are configured in the wine section. The drives are assigned according to the specifications made in the Drive sections.

```
[wine]
Windows=c:\windows
system=c:\windows\system
Temp=c:\tmp
```
