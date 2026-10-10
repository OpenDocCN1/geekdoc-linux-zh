
## 4) List the Components of the Virtual Partitions

From the **ioscan** and **dmseg** messages we can select the components of our first Virtual Partition. The following is a list of components we'll include in this partition:

First *vPar* *cable*
- name cable1
- processors min of one (bound) max of three (two unbound) with num (bound + unbound) equal to one
- memory 1024 MB
- LBA Core I/O 0/0 (all components on 0/0 are implied)
- LAN 0/0/0/0 (not specified explicitly, on 0/0)
- boot disk 0/0/1/1, 2, 0
- kernel /stand/vmmunix (this is default)
- autoboot off (manual)
- console 0/0/4/0 (not specified explicitly, on 0/0)

You may want to set *autoboot* to **auto** during installation and set to *manual* after installation. This makes booting easier during installation.

Some of the components require some explanation concerning the way in which they are implemented with vPars. The following is a more detailed discussion of some of these components, including CPU, memory, and LAN, bootdisk, setboot, kernel, and console.

### CPU

The CPUs used in both this partition (*cable1*) and the one we will define shortly (*cable2*) are specified with *min*, *max*, and *num*. We will have *min bound* CPUs that have I/O interrupts assigned to them and are therefore ideal for I/O-intensive applications. The additional CPUs assigned to the vPars are *unbound*, which do not process I/O interrupts. Therefore, *unbound* CPUs are ideal for processor-intensive applications as opposed to I/O-intensive applications. *unbound* CPUs can be freely moved from one vPar to another while vPars are running, so having *min bound* CPUs gives us the freedom to move around the unbound CPUs. Bound CPUs can also be added to and deleted from Virtual Partitions only when the partition is down.

On machines that employ Non-Uniform Memory Access (NUMA) you would use hardware paths (path) to specify CPUs. This is to ensure that you minimize the distance between CPUs and memory. On systems such as the N-Class and L-Class that do not employ NUMA, min is recommended to define bound CPUs.

There is detailed information on working with CPUs in Chapter 5. For our work on cable1 and cable2 and for my work with vPars in general, the most common desire is to have a min number of bound CPUs in all vPars and then move around unbound CPUs as the applications in vPars need them. For instance, when vparcreate is run we would specify the following:

```
vparcreate -p cable1 -a cpu:::1:3 -a cpu::1
```

At the time of creation cable1 will have one bound CPU only because we specified a min of one and a num of one. num is the total bound + unbound CPUs and since we specified one for num, we'll get one bound CPU (I have seen some vPars material use num and some use total so num and total are interchangeable in this book.) Since max is three we have left the door open to add as many as two additional unbound CPUs. If we have two unbound CPUs on our system, we can move them among the vPars as required with vparmodify. To remove the two unbound CPUs from cable2 and add them to cable1, we would issue the two following vparmodify commands:

```
vparmodify -p cable2 -m cpu::1		# reduces cable2 from 3 to 1
vparmodify -p cable1 -m cpu::3		# increases cable1 from 1 to 3
```

We first removed the two unbound CPUs from cable2 and then added them to cable1. If the two unbound CPUs were not assigned to a vPar, we would not have to remove them from cable2 prior to adding them to cable1.

There are many ways to work with CPUs, some of which are described in Chapter 5, so by characterizing your applications and understanding the options for using bound and unbound CPUs, you can use the processor mix that best meets you needs.

### Memory

We have identified one GByte of memory for *cable1*. Memory can be specified by *range* or *size*.

To add one GByte of memory to *cable1* using *size* we would use the following *vparcreate* command:

```
vparcreate -p cable1 -a mem::1024
```

This *vparcreate* command specifies only the memory for use in *cable1*. The full **vparcreate** command for creating *cable1* will be shown in an upcoming section.

The memory is specified in MBytes (1024 MBytes = 1 GByte) in multiples of 64 MBytes. At the time of this writing, the Virtual Partition Monitor consumes roughly 128 MBytes of RAM, so this will not be available to allocate to a Virtual Partition. Modifying memory allocation requires that the Virtual Partition be down at the time of this writing.

On machines that employ Non-Uniform Memory Access (NUMA) you would use the *range*. *Range* is a subset of *size*. On systems such as the N-Class and L-Class that do not employ NUMA, the *size* is recommended to define memory. The syntax for specifying memory by range is as follows:

```
mem:::base::range
```

None of the examples in this book were prepared using NUMA systems so you won't see any examples using the *range* syntax; all examples use the *size* syntax.

### LAN

The LAN interface used for this first Virtual Partition is on Local Bus Adapter (LBA) zero. This means that any other components on LBA zero would have to be in this Virtual Partition as well. At the time of this writing, components on an LBA can't be shared between vParS.

![](img/eff8b9287a5f38c5adf538f24aacf29e_118_0.png)

Note that we have decided not to use the hostname as our Virtual Partition name. As mentioned earlier, it is desirable to use the same name for the hostname and vPar. Because our hostnames are a little hard to remember the system administrator decided to use simple vPar names. When we loaded HP-UX 11i on the system we selected the hostnames (you can also run set_parsns after loading 11i to set the system name and other parameters) of cvhdcn3 and cvhdcn4. We then chose the simple vPar names of cable1 and cable2, respectively.

### Boot Disk

The ioscan issued earlier in this Chapter showed many disk devices. The boot device for our first Virtual Partition is the internal disk with the hardware path 0/0/1/1/2.0.

At the time of this writing, components that are at or below the Local Bus Adapter (LBA) level are devoted to a single Virtual Partition. This means that although the output of our earlier ioscan command shows four internal disks, all four of these disks must be in the same Virtual Partition because they are on the same LBA. Chapter 5 covers LBAs and hardware in more detail.

### Kernel

![](img/eff8b9287a5f38c5adf538f24aacf29e_119_0.png)

We'll use the default HP-UX kernel of /stand/vmunix for the kernel in this Virtual Partition. Since we're using the default kernel, we don't have to specify this as part of the vparcreate command, however, we'll include it in the vparcreate command for completeness purposes. Chapter 4 covers the HP-UX kernel.

### setboot Command

In our example we have autoboot set to off for our Virtual Partition. The set-boot command on a non-vPars system reads from and writes to stable storage. On a vPars system the setboot command interacts with the Virtual Partition database. In our upcoming example we'll set the autoboot to off when we create cable1 with vparcreate. Running setboot on a vPars system has the effects shown in Table 2-2:

| vPars setboot Option | Description |
| :--- | :--- |
| `-a` | Changes the alternate boot path of the Virtual Partition. <br> To set the alternate boot path: <br> `# setboot -a 0/8/0/0.8.0.5.0.0.0` |
| `-b` | Sets the autoboot attribute of the Virtual Partition. <br> To set Autoboot on: <br> `# setboot -b on` |
| `-p` | Changes the primary boot path of the Virtual Partition. <br> To set the primary boot path: <br> `# setboot -p 0/0/1/1.2.0` |
| `-s` | Has no effect. |
| `no options` | Displays information about boot attributes. |

The **setboot** command is one of the aspects of working with vPars that is different from a non-vPars system.

### Console

Chapter 5 contains a description of the way in which the console is implemented with vPars. In our first partition we have specified LBA 0/0 as a component of vPar cable1. Since the physical console at 0/0/4/0 is on the Core I/O card at 0/0, it is an implied component of cable1 and we do not have to specify the physical console in this partition. The other Virtual Partitions on this system will use the virtual console functionality of vPars whereby issuing Ctrl-A cycles between virtual console displays.
