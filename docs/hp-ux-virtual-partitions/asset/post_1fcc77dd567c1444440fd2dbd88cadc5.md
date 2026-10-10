
Protocol Adapter

ba 12 5/0/11 lba CLAIMED BUS_NEXUS Local PCI Bus Adapter (782)
ext_bus 3 5/0/11/0/0 c720 CLAIMED INTERFACE SCSI Ctrlx Fast Wide Differential
target 13 5/0/11/0/0.1 tgt CLAIMED DEVICE
disk 7 5/0/11/0/0.1.0 sdisk CLAIMED DEVICE HP DVD-ROM 3514K
target 14 5/0/11/0/0.3 tgt CLAIMED DEVICE
tape 0 5/0/11/0/0.3.0 stape CLAIMED DEVICE HP C1537A
target 15 5/0/11/0/0.7.0 tgt CLAIMED DEVICE
ctl 6 5/0/11/0/0.7.0 sctl CLAIMED DEVICE Initiator
ba 13 5/0/12 lba CLAIMED BUS_NEXUS Local PCI Bus Adapter (782)
ext_bus 4 5/0/12/0/0.0 c720 CLAIMED INTERFACE SCSI CB95 Fast Wide LVD
target 16 5/0/12/0/0.0 tgt CLAIMED DEVICE
disk 8 5/0/12/0/0.0.0 sdisk CLAIMED DEVICE SEAGATE ST318404LC
target 17 5/0/12/0/0.1 tgt CLAIMED DEVICE
disk 9 5/0/12/0/0.1.0 sdisk CLAIMED DEVICE HP 73.4GST373400SLC
target 18 5/0/12/0/0.2 tgt CLAIMED DEVICE
disk 10 5/0/12/0/0.2.0 sdisk CLAIMED DEVICE HP 73.4GST373400SLC
target 19 5/0/12/0/0.7 tgt CLAIMED DEVICE
ctl 7 5/0/12/0/0.7.0 sctl CLAIMED DEVICE Initiator
target 20 5/0/12/0/0.15 tgt CLAIMED DEVICE
ctl 8 5/0/12/0/0.15.0 sctl CLAIMED DEVICE HP AS572A
ba 14 5/0/14 lba CLAIMED BUS_NEXUS Local PCI Bus Adapter (782)
ba 15 5/0/14/0/0 cPCItoPCI CLAIMED BUS_NEXUS cPCItoGBT Bridge
lan 13 5/0/14/0/0/0.0 btlan CLAIMED INTERFACE HP AS5068 PCI 10/100Base-TX 4 Port
lan 14 5/0/14/0/0/0/5.0 btlan CLAIMED INTERFACE HP AS5068 PCI 10/100Base-TX 4 Port
lan 15 5/0/14/0/0/6/0 btlan CLAIMED INTERFACE HP AS5068 PCI 10/100Base-TX 4 Port
lan 16 5/0/14/0/0/7/0 btlan CLAIMED INTERFACE HP AS5068 PCI 10/100Base-TX 4 Port
memory 0 5/5 memory CLAIMED MEMORY Memory
processor 0 5/10 processor CLAIMED PROCESSOR Processor
processor 1 5/11 processor CLAIMED PROCESSOR Processor
processor 2 5/12 processor CLAIMED PROCESSOR Processor
processor 3 5/13 processor CLAIMED PROCESSOR Processor

Note that the ctl1 itself, which is for all intents and purposes a separate server, is at address 5. There are four processors, shown at the end of the listing, at 5/10, 5/11, 5/12, and 5/13. We're going to assign many of the I/O components in this listing to our four vPARs, so you may end up referring back to the diagram.

## Defining and Configuring the Four vPars

After having run the **ioscan** in the nPartition on our Superdome, we have determined that the following configurations will exist in our four vPars:

### vPar bvvpard1

- name: bvvpard1
- processors: min of one (bound) max of three (two unbound)
- memory: 2048 MB
- LBA Core I/O: 5/0/0 (all components on 0/0 are implied)
- LAN: 5/0/9
- boot disk: 5/0/12/0/0.0.0
- kernel: /stand/vmunix (this is default)
- autoboot: off (manual)
- console: on core I/O at 5/0/0

### vPar bvvpard2

- name: bvvpard2
- processors: min of one (bound) max of four (two unbound)
- memory: 2048 MB
- LAN: 5/0/14
- boot disk: 5/0/6/0/0.0.0
- kernel: /stand/vmunix (this is default)
- autoboot: off (manual)
- console: virtual

### vPar extappd2

- name: extappd2
- processors: min of one (bound) max of four (two unbound)
- memory: 2048 MB
- LAN: 5/0/3
- boot disk: 5/0/4/0/0.0.0
- kernel: /stand/vmunix (this is default)
- autoboot: off (manual)
- console: virtual

### vPar intappd2

- name: intappd2
- processors: min of one (bound) max of four (two unbound)
- memory: 2048 MB
- LAN: 5/0/2
- boot disk: 5/0/1/0/0.0.0
- kernel: /stand/vmunix (this is default)
- autoboot: off (manual)
- console: virtual

We have all the software we need on our vPars disks, including HP-UX, vPars software, patches, and so on.

Now that we have the full ioscans of all the components in the nPartition and have mapped out the components we'd like to have in our four vPars, we can issue the vpcreate commands to create the four vPars.

```bash
vpcreate -p bvvpard1 -B manual -b /stand/vmunix -a cpu:::1:3 \
-a mem::2048 -a io:5:0/9 -a io:5:0/12 -a io:5:0/12/0.0.0:boot \
-a io:5:0/0 -a io:5:0/11
```

```bash
vpcreate -p bvvpard2 -B manual -b /stand/vmunix -a cpu:::1:4 \
-a mem::2048 -a io:5:0/6 -a io:5:0/14 -a io:5:0/6/0.0.0:boot
```

```bash
vpcreate -p extappd2 -B manual -b /stand/vmunix -a cpu:::1:4 \
-a mem::2048 -a io:5:0/4 -a io:5:0/3 -a io:5:0/4/0.0.0:boot
```

```bash
vpcreate -p intappd2 -B manual -b /stand/vmunix -a cpu:::1:4 \
-a mem::2048 -a io:5:0/1 -a io:5:0/2 -a io:5:0/1/0.0.0:boot
```

These commands use the same form covered in chapters earlier in the book. Chapter 2 covered several examples of using vpcreate and its options. Notice that vPar bvvpard1 has in it the core I/O card at 5/0/0, which gives it console access, and the tape and DVD-ROM interface at 5/0/11, because this vPar will be used as an Ignite-UX server.

After having created and booted all four vPars, we can check the status of each and view their respective components with vparstatus -v as shown in the following listing:

```text
# vparstatus -v
[virtual Partition Details]
Name: bvvpard2 <-- vPar bvvpard2
State: Up
Attributes: Dynamic, Manual
Kernel Path: /stand/vmunix
Boot Opts:
```

![](img/eff8b9287a5f38c5adf538f24aacf29e_1025_0.png)

![](img/eff8b9287a5f38c5adf538f24aacf29e_1025_1.png)

```text
[CPU Details]
Min/Max: 1/4
Bound by User [Path]:
Bound by Monitor [Path]: 5.10
Unbound [Path]:

[IO Details]
5.0.6
5.0.12
5.0.0.1.0.0.0 BOOT

[Memory Details]
Specified [Base /Range]:
       (bytes) (MB)
Total Memory (MB): 2048
```

```text
[Virtual Partition Details] <<- vPar bvvpard1
Name:        bvvpard1
State:       Up
Attributes:  Dynamic, Manual
Kernel Path: /stand/vmunix
Boot Opts:
```

```text
[CPU Details]
Min/Max: 1/3
Bound by User [Path]:
Bound by Monitor [Path]: 5.11
Unbound [Path]:

[IO Details]
5.0.9
5.0.12
5.0.12.0.0.0.0 BOOT
5.0.0

[Memory Details]
Specified [Base /Range]:
       (bytes) (MB)
Total Memory (MB): 2048
```

```text
[Virtual Partition Details] <<- vPar extappd2
Name:        extappd2
State:       Up
Attributes:  Dynamic, Manual
Kernel Path: /stand/vmunix
Boot Opts:

[CPU Details]
Min/Max: 1/4
Bound by User [Path]:
Bound by Monitor [Path]: 5.12
Unbound [Path]:

[IO Details]
5.0.4
5.0.3
5.0.4.0.0.0.0 BOOT

[Memory Details]
Specified [Base /Range]:
(bytes) (MB):
Total Memory (MB) : 2048
```

```text
[Virtual Partition Details]
Name: intappd2 -- vPar intappd2
State: Up
Attributes: Dynamic, Manual
Kernel Path: /stand/vmunix
Boot Opts:

[CPU Details]
Min/Max: 1/4
Bound by User [Path]:
Bound by Monitor [Path]: 5.13
Unbound [Path]:

[IO Details]
5.0.1
5.0.2
5.0.1.0.0.0.0 BOOT

[Memory Details]
Specified [Base /Range]:
(bytes) (MB):
Total Memory (MB) : 2048
```

![](img/eff8b9287a5f38c5adf538f24aacf29e_1027_0.png)

We now have four vPars set up with the components that we have specified. The output of this vparstatus command is identical to that we viewed in the earlier L-Class and N-Class examples in the book except that the paths employed are those from a Superdome.

## The Console

We can use Ctrl-A to toggle between the four vPars on the console in the nPartition in which we're working. The console on the core I/O card at 5.0/0 in our nPartition is configured as part of vPar bvvpard1. Figure B-2 shows using Ctrl-A to toggle between the vPars using the console:

![](img/eff8b9287a5f38c5adf538f24aacf29e_1028_0.png)

Figure B-2 shows hitting Ctrl-A four consecutive times in order to switch the vPars virtual console between our four vPars, named intappd2, bvvpard2, bvvpard1, and extappd2. As covered earlier in the book, when you switch between vPars with Ctrl-A you are supplied with the name of the console-connected vPar in brackets.

Since each of the vPars has a LAN card associated with it, we can connect with Telnet to any of the vPars over the network as well as using the console in Figure B-2.

Keep in mind that the console we're using is for the entire Superdome complex. We selected the nPartition in which our four vPars are configured and then switched between the vPars with Ctrl-A.

We connect to the GSP of the Superdome complex using the IP address of the GSP. When we log in to the GSP, the top screen in Figure B-3 appears. We then issue CO, which produces a list of consoles for the nPartitions in the Superdome as shown on the bottom of Figure B-3:
