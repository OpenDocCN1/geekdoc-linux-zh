In smaller servers such as a DNS or small web server, it is sometimes simpler to use many of the default install options for SLES. One of the implications of such an installation is that the Logical Volume Manager (LVM) software is not used to configure the environment. LVM allows for the dynamic addition of disk capacity and targets the new disk to specific volume sets on a live system. Though very powerful, such configurations can get complex and will not be addressed in this section. Additional information on LVM can be found at a series of whitepapers on the SUSE website (http://www.suse.com/en/whitepapers/lvm/lvm1.html).

Before you add a disk device to a system, it is important to know where you are going to target the device. When you’re building a system, it is good practice to separate, on different devices or partitions, various portions of the directory structure. If, at any point, your / partition becomes 100% used, your system will not be able to operate.

Segregation of the major branches of the / directory help mitigate accidental consumption of critical disk space. Typically, the / level directory on your SLES server contains the entries in the following listing:

```
Athena:~ # ls /
.    bin   dev   home   lost+found   mnt   proc   sbin   sys   usr
..   boot   etc   lib   media       opt   root   srv   tmp   var
Athena:~ #
```

When you are building a server (see Chapter 1, “Installing SUSE LINUX Enterprise Server”), you have the opportunity of allocating these directories to different locations. On a simple one-disk device system, the default install splits the volume into a swap and a / partition. A more robust approach would be to further partition the single volume into distinct areas to contain the more volatile directory structures. On servers that allow end-user content, placing the /home (user files) and /srv (web content) directories on their own device will balance disk consumption across multiple volumes. If individual devices are not available, placing /home and /srv on separate partitions is still a good idea. The segregation will prevent consumption on one partition from impacting the other. Though you can minimize the risks of a disk-full event through quota management, making the system failsafe is simply the smart thing to do.

# Adding a Disk

In our example, a disk will be added to the web server Athena. The current web server will be asked to store a large number of corporate documents