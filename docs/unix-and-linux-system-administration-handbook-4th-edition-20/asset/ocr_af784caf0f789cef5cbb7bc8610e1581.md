# Chapter 24 Virtualization

Before you create a virtual machine, its storage and network resources must be available. In the example below, we first create a filesystem on one of the host's physical disks to store the guest, then create a vswitch to provide the guest's network-connectivity. To summarize the virtual creation process:

+   - Create a storage resource for the guest's files.
- Create a virtual switch for network connectivity.
- Create the virtual machine.
- Start and install the virtual machine.

In the series of commands below, we use the mkfs command to create a filesystem on the physical device disk3, an arbitrary disk that happened to be available on our lab system. It will eventually store the guest's operating system, applications, and data. The file is mounted under /dev/, and finally the hpvmdevmgmt creates a storage entity called disk1.

```
hpux-$# sudo mount -F vxfs -o largefiles /dev/dev/disk3
hupx-$# sudo mount /dev/dev/disk3 /dev/vm0disk/
hupx-$# sudo hpvmdevmgmt -S 8G /dev/vm0disk/disk1
```

The next step is to create a virtual switch for the guest. A single vswitch can be used by multiple guests.

| Station | Crd Hdw | Net-Interface | NM | MAC | HP-DLPI | DLPI |
| Path | Address | Inf State NamePPA | ID Type Support | |
| 0/0/0 | 0x00306EEAA927 | 0 UP | lan0 snap0 | 1 ETHER Yes | 119 |
| 0/1/2 | 0x00306EEAA720D | 0 UP | lan1 snap1 | 2 ETHER Yes | 119 |

```
hpux-$# sudo hpvmnet -c -S vm0switch -n 0
hupx-$# sudo hpvmnet -b -S vm0switch
```

Here, the handy lancan command finds all the system's network interfaces. We need the identifier for the network interface on the correct network; it's the 0 in. Using the hpvm command, we create the switch by using lan0, start it in the next command with the -b argument.

Now that the necessary resources have been created, it's finally time to create the virtual machine.

```
hpux-$# sudo hpvmcreate -P vm0 -O hit -r 2G
-a network:lan0:vswitch:vm0switch -a device:scsi:/dev/vm0disk/disk1
hupx-$# sudo hpvmstart -P vm0
```

This command creates a virtual machine vm0, allocates 2GB of memory for it, uses the virtual switch vm0switch, and selects the storage device we created above. The new virtual machine is started with the hpvmstart command.

Installation of the virtual machine is identical to installing a physical machine from the console. To access the console with hpvmconsole -P vm0 and disconnect with <Control-B>. To check the status of a guest, use hpvmstatus -P vm0.