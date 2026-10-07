
## Chapter 21: Upgrading Linux Kernels and Software Packages

The make utility is used when you need to change your Linux kernel. This is called remaking the kernel. For example, if you need only to add a feature that hasn't been enabled on your system, it may take less time to remake the kernel than if you install an entirely new kernel from the Internet, because only certain parts of the operating system code must be recompiled.

A file, called Makefile, is associated with each program that will be compiled (made) using the make utility. This Makefile usually includes labels that define different things that the make utility can do. For example, there might be a depend label to prepare all dependent files, or an install label to get everything ready to use the program after the main compilation is completed. The documentation for a program that you download from the Internet will include instructions on preparing the source code files. For example, it might include instructions like the following example:

- 1. Use this command to untar the source code archive:

```
tar xvf newprogram.tar
```

- 2. Be certain you are in the main program directory, then make the program with this command:

```
make
```

- 3. Finally, before using the program, use this command:

```
make install
```

The make utility always looks for a file called Makefile in the current directory and uses the instructions in it. By using the make utility, you never have to execute the c compiler in Linux — just remake the Makefiles that are included with the programs that you download.

## Creating a New Linux Kernel

Recompiling the Linux kernel isn't so difficult. Just log in as the root user and follow these steps:

- 1. Start by making a backup of the existing kernel image in case something goes wrong. Use a command like this:

```
cp /vmlinux vmlinux.old
```

- 2. Change to the Linux source directory so that the make utility will locate the correct Makefile:

```
cd /usr/src/linux
```

- 3. Configure the kernel using this command:

```
make config
```

# 458 Linux Web Server Toolkit

Answer all the questions that appear on the screen for which features to include. There are over 50, but you can just press Return again and again to choose the default (capitalized) option. A sample of these questions as they scroll down the screen is shown in Figure 21-1.

Using the command make menuconfig make x may make this process easier as you learn about the Linux kernel.

![](img/e01f1106dd2902613fa07890c8baa7e6_485_0.png)

- Networking options
Network firmware (CONFIG_IP_FIRMWARE) [Y/n]
- Network aligning (CONFIG_IP_NET_ALIGN) [Y/n]
- IP networking (CONFIG_IP) [Y/n]
- IP ARP (CONFIG_IP_ARP) [Y/n]
- Multicasting (CONFIG_IP_MULTICAST) [Y/n]
- MTU (transmission Unit) [Y/n]
* It is safe to leave these unless you understand

* TCP/IP compatibility mode (CONFIG_TCP_MATCH)
* Path MTU Discovery enabled (CONFIG_IP_MTU_DISCOVERY) [Y/n]
* IP Forwarding (CONFIG_IP_FORWARDING) [Y/n]
* IP large windows (not recommended unless memory of system is large) (CONFIG_IP_LARGE_WINDOW) [Y/n]

* The TCP protocol (CONFIG_TCP) [Y/n]
- IPv4 stack (CONFIG_IP_STACK) [Y/n]
- Kernel/router network link driver (CONFIG_NET_LINUX) [Y/n]
* 64-bit support
- NDIS drivers (CONFIG_NET_NDIS) [Y/n]
- Network device
- Network device support (CONFIG_NET_DEVICES) [Y/n]
- Serial line load balancing (CONFIG_SERIAL_EQUIVALENT) [Y/n]
- SLIP line protocol (CONFIG_NET_SLIP) [Y/n]
- PPP point-to-point (CONFIG_PPP_P2P) [Y/n]
- PPP dialup control (CONFIG_PPP_DIAL) [Y/n]
- Ethernet or serial (CONFIG_NET_ETHERNET) [Y/n]
- Bridge support (CONFIG_NET_BRIDGE) [Y/n]
- Socket support (CONFIG_NET_SOCKET) [Y/n]
- SCTP (CONFIG_NET_SCTP) [Y/n]
- SOCKS support (CONFIG_NET_SOCKS) [Y/n]
- Network-specific cards (CONFIG_NET_SPECIALLY) [Y/n]
- Other network cards (CONFIG_NET_OTHER) [Y/n]

| | | | |
|---|---|---|---|
| algogen | 25/tcp | tquery support | |
| amqp | 25/tcp | | |
| hitdata | 29/tcp | | |
| ipfilter | 32/tcp | * default flip data | |
| ipv6 | 32/tcp | | |
| packet | 32/tcp | | |
| qnet | 32/tcp | mail | |
| rnetd | 32/tcp | | |
| time | 32/tcp | resources | |
| timer | 32/tcp | * | |
| namesserver | 52/tcp | | |
| rerror | 52/tcp | | |
| uaccess | 52/tcp | * 100IT server | |
| bootps | 67/udp | * client | |
| bounce | 69/udp | * Internet Charger | |
| boston | 69/udp | | |
| bntp | 70/tcp | | |
| ftp | 21/tcp | | |
| rlogin | 77/tcp | netria | |
| finger | 79/tcp | | |
| www | 80/tcp | World Wide | |
| http | 80/tcp | Hypertext | |
| nip | 88/tcp | | |
| kerberos | 88/tcp | * Kerberos | |

Figure 21-1: You configure the kernel by answering a set of questions about which features should be included or enabled in the newly compiled kernel.

4. This command to set up all the dependencies correctly:
```
make dep; make clean
```

## Chapter 21: Upgrading Linux Kernels and Software Packages

5. Compile the kernel by entering this command (it may take up to an hour or more to completely compile the kernel, depending on the kernel,):

```
make
```

6. Finally, before using the program, use this command:

```
make install
```
