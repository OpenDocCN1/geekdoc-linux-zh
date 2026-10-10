
## The Root Filesystem

Before the advent of Linux distributions, it used to be a project by itself to put together a compact application-set tailored to suit the size limitations of available storage. One had to cobble together the sources of a minimal set of utilities, *libraries*, tools, and *daemons*; ensure that their versions liked each other; and cross-compile them. Today’s distributions supply a ready-made application-set built for supported processors and offer tools that let you pick and choose components at the granularity of packages. Of course, you may still want to implement custom utilities and tools to supplement the distribution-supplied applications.

On embedded devices, flash memory (discussed in Chapter 17) is the commonly used vehicle to hold the application-set and is mounted as the root device at the end of the boot process. Hard disks are uncommon because they are power-intensive, bulky, and have moving parts that are not tolerant to shock and vibration. Common places that hold the root filesystem on embedded devices include the following:

- An initial ramdisk (*initramfs* or *initrd*) is usually the starting point before you get drivers for other potential root devices working and is used for development purposes.
- NFS-mounting the root filesystem is a development strategy much more powerful than using a ramdisk. We discuss this in detail in the next section.
- Storage media such as flash chips, SD/MMC cards, CF cards, DOCS, and DOMs.

Note that it may not be a good idea to let all the data stay in the root partition. It’s common to spread files across different storage partitions and tag desired *read-write* or *read-only* protection flags, especially if there is the possibility that the device will be shut down abruptly.

## NFS-Mounted Root

NFS-mounting the root filesystem can serve as a catalyst to hasten the embedded development cycle. In this case, the root filesystem physically resides on your development host and not on the target, so its size is virtually unlimited and not restricted by the amount of storage locally available on the target. Downloading device driver modules and applications to the target, as well as uploading logs, is as simple (and fast) as copying them to /path/to/target/rootfilesystem/ on your development host. Such ease of testing and debugging is a good reason why you should insist on having Ethernet on engineering-level hardware, even if production units won’t have Ethernet support. Having Ethernet on your board also lets your bootloader use the Trivial File Transfer Protocol (TFTP) to download the kernel image to the target over a network.

Table 18.2[^4] shows the typical steps needed to get TFTP and NFS working with your embedded device. It assumes that your development host also doubles up as TFTP, NFS, and DHCP servers, and that the bootloader (BLOB in this example) supports the Ethernet chipset used on the embedded device.

> [^4] The filenames and directory path names used in Table 18.2 are distribution-dependent.

**Table 18.2. Saving Development Time with TFTP and NFS**

| | Target Embedded Device | Host Development Platform |
|---|---|---|
| Kernel Boot over TFTP | Configure the IP address of the target and the server (host) from the bootloader prompt:<br>`/* Target IP */`<br>`blob> ip 4.1.1.2`<br>`/* Host IP */`<br>`blob> server 4.1.1.1`<br>`/* Kernel image */`<br>`blob> TftpFile /tftpdir/zImage`<br>`/* Pull the Kernel over the net */`<br>`blob> tftp`<br>`TFTPing /tftpboot/zImage ... Ok`<br>`blob>` | Configure the host IP address:<br>`bash> ifconfig eth0 4.1.1.1`<br>Install and configure the TFTP server (the exact steps depend on your distribution):<br>`bash> cat /etc/xinetd.conf/tftp`<br>`service tftp`<br>`{`<br>`    socket_type = dgram`<br>`    protocol = udp`<br>`    wait = yes`<br>`    user = root`<br>`    server = /usr/sbin/in.tftpd`<br>`    server_args = /tftpdir`<br>`    disable = no`<br>`    per_source = 11`<br>`    cps = 100 2`<br>`    flags = IPv4`<br>`}`<br>Make sure that the TFTP server is present in `/usr/sbin/in.tftpd` and that `xinetd` is alive. |
| Root filesystem over NFS | `blob> boot console=/dev/ttyS0,115200n8 root=/dev/nfs ip=dhcp`<br>`/* Kernel boot messages */`<br>`/* . . . . */`<br>`VFS: Mounted root (nfs filesystem)`<br>`/* . . . . */`<br>`login:` | Compile the target kernel with NFS enabled and copy it to `/tftpdir/zImage`.<br>Export `/path/to/target/root/` for NFS access:<br>`bash> cat /etc/exports`<br>`/path/to/target/root/ * (rw,sync,no_root_squash,no_all_squash)`<br>Start NFS:<br>`bash> service nfs start`<br>Configure the DHCP server. The kernel on the embedded device relies on this server to assign it the 4.1.1.2 IP address during boot and to supply `/path/to/target/root/:`<br>Code View:<br>`bash> cat /etc/dhcpd.conf`<br>`...`<br>`subnet 4.1.1.0 netmask 255.255.255.0 {`<br>`    range 4.1.1.2 4.1.1.10`<br>`    max-lease-time 43200`<br>`    option routers 4.1.1.1`<br>`    option ip-forwarding off`<br>`    option broadcast-address 4.1.1.255`<br>`    option subnet-mask 255.255.255.0`<br>`    group {`<br>`        next-server 4.1.1.1`<br>`        host target-device {`<br>`            /* MAC of the embedded device */`<br>`            hardware Ethernet AA:BB:CC:DD:EE:FF;`<br>`            fixed-address 4.1.1.2;`<br>`            option root-path "/path/to/target/root/";`<br>`        }`<br>`    }`<br>`...`<br>`}`<br>`bash> service dhcpd start`<br>`bash>` |

## Compact Middleware

Embedded devices that are tight on memory prefer middleware implementations that have small footprint and low runtime memory requirements. The trade-offs usually lie in features, standards compatibility, and speed. Let's take a look at some popular compact middleware solutions that may be potential candidates for populating your root filesystem.

*BusyBox* is a tool commonly used to provide a multi-utility environment on embedded systems having limited memory. It scratches out some features but provides an optimized replacement for several shell utilities.

*uClibc* is a compact version of the GNU C library that was originally developed to work with uClinux. uClibc works on normal Linux systems, too, and is licensed under LGPL. If your embedded device is short on space, try uClibc rather than glibc.

Embedded systems that need to run an X Windows server commonly rely on *TinyX*, a low-footprint X server shipped along with the XFree86 4.0 code. TinyX runs over frame buffer drivers and can be used on devices, such as the one showed in Figure 12.6 of Chapter 12.

*Thhttpd* is a lightweight HTTP server that makes low demands on CPU and memory resources.

Even if you are creating a non-Linux solution using a tiny 8-bit MMU-less microcontroller, you will likely want it to interoperate with Linux. Assume, for example, that you are writing deeply embedded firmware for an Infrared storage keychain. The keychain can hold a gigabyte of personal data that can be accessed via a web browser from your Linux laptop over Infrared. If you are running a compact TCP/IP stack, such as *uIP* over a minimal IrDA stack such as *Pico-IrDA* on the Infrared keychain, you have the task of ensuring their interoperability with the corresponding Linux protocol stacks.

Table 18.3 lists the home pages of the compact middleware projects referred to in this section.

### Table 18.3. Examples of Compact Middleware

| Name | Description | Download Location |
|---|---|---|
| BusyBox | Small footprint shell environment | www.busybox.net |
| uClibc | Small-sized version of glibc | www.uclibc.org |
| TinyX | X server for devices that are tight on memory | Part of the X Windows source tree downloadable from ftp://ftp.xfree86.org/pub/XFree86/4.0/ |
| Thhttpd | Tiny HTTP server | www.acme.com/software/thttpd |
| uIP | Compact TCP/IP stack for microcontrollers | www.sics.se/adam/uip |
| Pico-IrDA | Minimal IrDA stack for microcontrollers | http://blaulogic.com/pico_irda.shtml |
