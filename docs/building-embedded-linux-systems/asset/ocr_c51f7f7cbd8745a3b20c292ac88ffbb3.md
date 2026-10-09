# # Booting Using BOOTP/DHCP, TFTP, and NFS

If you have properly configured a server to provide the target with DHCP, TFTP, and NFS services, as we explained earlier, you can boot your target remotely. This allows you to quickly make changes to the root file system without lengthy reflashing cycles to the device. It also allows you to share the root file system between the device itself (usually not an ideal development environment) and a fully featured development host that can mount the same file system (on a different mountpoint) at the same time.

> **A Note About Networking and the GTA01**
> 
> The OpenMoko GTA01 reference hardware used in this chapter doesn’t have a real Ethernet adapter, so it cannot boot directly over a network from within U-Boot itself. This means that U-Boot on the GTA01 does not contain built-in support for commands such as *bootp*. Instead, GTA01 developers have created a special fake network interface built upon support already present within Linux kernels for USB “gadgets.” This allows OpenMoko developers to instruct the Linux kernel to mount its root file system over the special emulated network running over USB, but only once the kernel itself has booted. As a consequence of this, the network boot examples in this section are actually based upon another reference hardware platform from Xilinx, the ML403. Further information about configuring this board and examples of its use are also included on this book’s website.

U-Boot contains a variety of commands (depending upon its build-time configuration) that are useful for booting over a network. One of these is the *bootp* command. It no longer actually uses the original BOOTP protocol but instead supports the modern DHCP alternative. The following output was taken from a development board that does have a built-in network interface, performing a *bootp* command:

```
```text
=> bootp
DHCP client bound to address 192.168.1.202
TFTP from server 192.168.1.3; our IP address is 192.168.1.202
Filename '/tftpboot/ulmage-2.6.24.img'.
Load address: 0x100000
Loading: ##################################################
#####################################################
#####################################################
done
```
```

The *bootp* command issues a request that is answered by the DHCP server. Using the DHCP server’s answer, U-Boot contacts the TFTP server and obtains the Linux kernel image file, which it places at the configured load address in the target RAM.

After an image has been loaded (either over the network, serial console, or via any other means), you can verify the image’s header information using the *minfo* command. For example, on our GTA01 reference hardware: