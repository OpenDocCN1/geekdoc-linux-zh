
To configure your SCSI scanner, you should have support for generic SCSI devices in your kernel. To do this, follow these steps:

- 1. Log in as root.
- 2. Change the directory to the Linux kernel sources directory:
  `#cd /usr/src/linux`
- 3. Start the kernel's configuration modules by typing the following:
  `#make menuconfig`
- 4. The kernel configuration module will start; navigate to SCSI Support and press Enter.
- 5. Highlight SCSI Support and press Y to include it in your kernel.
- 6. Highlight SCSI Generic Support and press Y to include it in your kernel.
- 7. Press Esc twice to exit the SCSI Support menu.
- 8. Press Esc twice again to exit the kernel configuration module. It will ask you whether you want to save your new kernel configuration; choose Yes.
- 9. Now you need to recompile your kernel for these changes to take effect. To do so, type in the following commands, one after the other:
  `#make dep`
  `#make clean`
  `#make bzImage`
  `#make modules`
  `#make modules_install`
- 10. Each of these commands will take some time to execute, and a lot of text will scroll by—don't worry, this is normal. When all the commands have executed, reboot your system.

Now you need to check for your scanner by using the sgcheck command. Run the command like this:

```
# sgcheck
```

The command will give you a list of all the SCSI devices on your system. Your scanner should have an entry with the word Processor or Scanner somewhere in it. For example,

```
Assignment of generic SCSI devices,
device host/channel/ID/LUN type(numeric type) vendor model:
/dev/sg0 0/0/0/0 CD-ROM IOMEGA ZIPCD 4x650
/dev/sg1 0/0/5/0 Processor(3) HP C2500A
```

As you can see, the scanner here is /dev/sg1. You now can proceed to use YaST to configure that scanner. To do that, follow these steps:

- 1. Log in as root.
- 2. Run YaST.
- 3. Navigate to System Administration, Integrate Hardware Into System, Configure Your Scanner and press Enter.
- 4. The Scanner Configuration module will load. The first option is the SCSI device list. YaST will show you a list of all the generic SCSI devices on your system. Select /dev/sg1 and press Enter.
- 5. Next, YaST will show you a list of all the supported scanners; choose yours from the list and press Enter.
- 6. Press Continue to save your configuration.
- 7. YaST then will run SuSEConfig to finalize the configuration.

That is all you need to do to set up your scanner. You now can use xscanimage to scan images from your scanner and save them as image files. Run xscanimage from within the X Window System, from an X terminal like the following and start scanning:

```
$xscanimage
```

## TV Cards

Recently, a large number of TV cards have begun appearing on the market. These cards, which are relatively inexpensive, enable you to watch TV on your computer. Linux has support for quite a few of these cards. This support is made available by the bttv kernel modules and package.

SuSE has prepared its distribution very well for TV cards. The first thing you should do is make sure that you have support for bttv in your kernel. This is not necessary if you haven't changed the kernel that is installed by SuSE. To configure your kernel, follow these steps:

- 1. Log in as root.
- 2. Change the directory to the Linux kernel sources directory:
  `#cd /usr/src/linux`
- 3. Start the kernel's configuration modules by typing the following command:
  `#make menuconfig`
- 4. The kernel configuration module will start; navigate to Character Devices, Video For Linux and press Enter.
- 5. Highlight Video For Linux and press M to include it in your kernel as a module.
- 6. Do the same for all the rest of the options in the list, making them all modules.
- 7. Press Esc twice to exit the Video For Linux menu.
- 8. Press Esc twice to exit the Character Devices menu.
- 9. Press Esc twice again to exit the kernel configuration module. It will ask you whether you want to save your new kernel configuration; choose Yes.
10. Now you need to recompile your kernel for these changes to take effect. To do so, type in the following commands, one after the other:

```
#make dep
#make clean
#make bzImage
#make modules
#make modules_install
```

11. Each of these commands will take some time to execute, and a lot of text will scroll by—don’t worry, this is normal. When all the commands have executed, reboot your system.

Now, you should install the bttv package from your SuSE Linux CDs.

**Package requirements:**

**Series gra:**

- bttv

When you are finished installing the package, run the configuration tool located in /usr/doc/packages/bttv/tools:

```
# cd /usr/doc/packages/bttv/tools
# ./update
```

This command will detect your TV card and configure the system to use it. When it's finished, you can watch TV by running the xtvscreen program. Run it from within the X Window System, from an X terminal, like this:

```
$xtvscreen
```

That's it! You now can enjoy your TV.

## Troubleshooting

*I run cdrecord -scanbus, but I don't see my CD-R/RW.*

This is probably because you did not configure your drive correctly. If it is a SCSI CD-R/RW, make sure you have support for SCSI CD-ROMs and your SCSI controller in the SCSI low-level drivers. If it is an IDE drive, make sure ATAPI/IDE CD-ROM support is a module, not built in.

## I can't mount my Zip drive.

Make sure you loaded the module by running one of the following commands:

```
#modprobe imm
```

```
#modprobe ppa
```

Also, make sure that your drive is on and has a disk in it.

## My joystick/gamepad is not detected!

Make sure that your sound card is configured as well. In addition, make sure that you have the correct joystick/gamepad configured in the kernel.

## Network Configuration

- 13 Configuring a TCP/IP Network 269
- 14 Configuring Domain Name Service 285
- 15 Connectivity with Windows Through Samba 301
- 16 Connectivity with Other Operating Systems 321
- 17 Configuring a Usenet News Service 337
- 18 Setting Up the Apache Web Server 345
- 19 Configuring the FTP Server 359
- 20 Configuring the Mail Server 371
- 21 Configuring the Dial-In Server 377
- 22 Setting Up SuSE Linux as a Proxy Server 391
- 23 Connectivity to the Internet 405

## Configuring a TCP/IP Network

## In this chapter

- Networking in SuSE Linux 270
- Understanding TCP/IP Networking 270
- What You Need to Know to Get Connected 271
- Using YaST to Configure Your Network 272
- Upgrading or Changing Your Network Card 277
- Network-Related Configuration Files 278
- Securing Your Network Using a Firewall 278
- Troubleshooting 284

## Networking in SuSE Linux

Connected seems to be the buzzword these days. When was the last time you saw a PC that was totally disconnected from some kind of network? Being connected to a network, even if it's for a short while, is the norm these days. If you are not connected to a local area network, you most likely are connected to the Internet, or both. Linux was built with the help of the Internet. This, along with the fact that it gets its roots from UNIX, makes it a perfect platform for networks. Linux supports almost all widely used networking protocols and devices. Being on a network with Linux feels very familiar. Even when Linux is on a standalone machine, it uses networking architectures in many of its applications—for example, the X Window System.

Connecting to a network using SuSE Linux is easy. This chapter explains how to configure SuSE Linux to get connected to a local area network using TCP/IP and an Ethernet card. You should take a minute to understand how TCP/IP works; it will help when you configure your system.

## Understanding TCP/IP Networking

In 1969, TCP/IP was developed by the United States Defense Advanced Research Projects Agency (DARPA). The protocol was developed for an experimental network known as ARPAnet. TCP/IP was adopted as the standard protocol to use, and ARPAnet eventually became the Internet.

The structure of a TCP/IP network is not very complex. Every machine connected to a network must have what is called an IP address. An IP address is a number in the format xxx.xxx.xxx.xxx—for example, 192.168.12.19—that uniquely identifies a machine on the network.

The IP address can be—but is not always—mapped to what is called a hostname. A hostname helps give your machine an easy-to-remember text name.

You can give your machine any name you want, as long as it is unique in the network to which you are connected. For example, you can call your machine suselinux as long as no other machine in your network is called suselinux. Please note that you can have a machine that has no hostname; it is not a necessity.

When you want to access a computer outside your network, you have to make that request to a gateway. A gateway is a computer or router that links different networks together, passing data packets back and forth between them.

All communication among machines is done via their IP addresses using one of the common protocols such as TCP or UDP.
