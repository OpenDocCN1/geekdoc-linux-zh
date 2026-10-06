
## 3.4.2 Loading in your hardware modules

You can determine what modules are loaded with the command `lsmod` as in Figure 69. This will list the modules that have been loaded. It is actually the same as the `/proc/modules` file that is listed in the directory listing in Figure 68.

| lsmod | Size | Used by |
| --- | --- | --- |
| nfsd | 141194 | 8 (autoclean) |
| nfs | 377904 | 1 (autoclean) |
| lockd | 29112 | 1 (autoclean) [nfs nfs] |
| sunrpc | 48700 | 1 (autoclean) [nfs nfs lockd] |
| pnet32 | 9094 | 0 |
| ibcs | 115616 | 0 |
| parport_probe | 2940 | 0 (autoclean) [unused] |
| ip | 4960 | 0 (unused) |
| parport | 6676 | 0 [parport_probe lp] |
| vfat | 9092 | 0 (unused) |

Figure 69. The lsmod command

If you need to add a module, you can determine the module name by going to the directory `/lib/modules` as you see in Figure 70.

```bash
[root@redhat ~]# cd /lib/modules
[root@redhat modules]# ls
```

```
2.2.16-22
[root@redhat modules]# cat 2.2.16-22
block cd misc modules.dep pcmia scsi uisbd
35c0.0 cm20020.0 e3210.0 me2k-pci.0 slhc.0
35c0.0 cms90.eth0 ns3210.0 slip.0
35c1.0 cms260.eth1 ni650.0 smc-mca.0
35c7.0 copsa_0 f8x88.ni152.0 smc-ultra.0
35c9.0 cssa.0 hardvill.ni650.0 smc-ultra-32.0
35d1.0 ca9b0.00 oymepc.0 scsi34.0
35e23.0 de4e0.0 hp-lp32.0 pcmnet32.0
35e27.0 de0e0.0 hp-lp100.0 pip.0
35f01.0 de00.0 ibtr.0 tian.0
35f26.0 de5e0.0 ipq6.0 pellate.0 tulip.0 vi-chra.0
8196.0 dprc.0 1rda.0 rtb8139.0 wasnipe.0
ac3200.0 dlci80.0 isrdm.0 sh8000.0 wavelan.0
arc-iscn.0 eth10.0 sdla.0.adrv.0 wide.0
alrian-pro.0 eqx01.0 in3930.0 x25_asay
elarpas.0 espr0.0 shepher.0 yellowfin.0
at1700.0 epic100.0 sk_mca.0 285230.0
bsd_comp.0 epl1.0 sktr.0
```

Figure 70. Finding loadable hardware modules

The file that you need to load is the `/etc/modules.conf`. This file contains the list of modules that you will load when you boot the system. It contains aliases, such as `eth0`, which are linked to the names of actual modules that are loaded. Also it contains options that you might need to load to make certain hardware work in Linux. When you want a module to be included on the boot sequence you can add it to this file. For example, to add an IBM ISA token-ring device on boot, create the entry:

Add the line in the `/etc/modules.conf` file and the module will be loaded on bootup.

```bash
# /etc/modules.conf
alias eth2 pcmnet32
alias eth0 pcmnet32
alias net0-4 off
alias char-major-14 sb
options sb 0x0220 irq=5 dma=1-6 mpu_io=0x0330
#
```

Figure 71. /etc/modules.conf file

64 Linux System Administration and Backup for IBM @server xSeries and Netfinity

## 3.4.3 Setting up your network

You first need to verify Linux recognized your network hardware. You can look at the resources listed in 3.4.1, "Determining the hardware" on page 61. If you do not see it, you need to verify that the hardware is set up properly. You can go to the manuals that the hardware or if the manufacturer has other information available. Then you need to see if the hardware is supported. To select the supported entries to get the hardware compatibility list for your current version of Red Hat Linux, go to:

```
http://www.redhat.com
```

You can determine which network cards have modules loaded by looking at Figure 69 on page 63. If you do not see the modules for your network card, you need to manually load the module or modules with the following command:

```bash
insmod module_name
```

Where the module_name is selected from those in Figure 70. If you do not see the module for your specific hardware device then you can do research on the Internet. Besides `http://www.redhat.com`, you should try the Web site for the manufacturer of the hardware you are using. Many manufacturers are making it a point to include support for Linux.

Once the module is successfully loaded, you can add it to the `/etc/modules.conf` file as discussed earlier and it will be loaded on bootup.

Once have all modules loaded, either automatically or manually, you need to determine that networking is in place. To see all of the network devices that have been recognized and have had their modules loaded, type the command:

```bash
ifconfig
```

If this is a new device for TCP/IP you may find that some items such as the inet address need to be defined.

```
ifconfig
eth0: flags=BROADCAST,BROIC,MULTICAST,LOOPBACK,UP,RUN  MTU=1500  ether 00:00:00:00:00:00
   inet 192.168.1.1  netmask=255.255.255.0  broadcast=192.168.1.255
   inet6 fe80::2ff:fe00:0:0/64  scope=link 
                                  txquelen=1000  packets=0  transmitted=0  errors=0  dropped=0
```
