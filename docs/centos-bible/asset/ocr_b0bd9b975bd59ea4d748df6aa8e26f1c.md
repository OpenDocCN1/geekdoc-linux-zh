# ## Configuring Modules

In a perfect world, after installing and booting Linux, all of your hardware should be detected and available for access. While CentOS systems are rapidly moving closer to that world, there are times when you must take special steps to get your computer hardware working.

CentOS systems come with tools for configuring the drivers that stand between the programs you run (such as CD players and Web browsers) and the hardware they use (such as CD-ROM drives and network cards). The intention is to have only the most critical drivers your system needs built into the kernel; these are called *resident drivers*. Other drivers that are added dynamically as needed are referred to as *loadable modules*. The trend is to keep the basic kernel as lean as possible, so that each running system has only a few resident drivers and it can dynamically add what it needs.

# ### Listing Loaded Modules

To see which modules are currently loaded into the running kernel on your computer, you can use the `lsmod` command. Here's an example:

```
```
# lsmod
Module                 Size  Used by
snd_seq_oss            38912   0
snd_seq_midi_event      9344   1 snd_seq_oss
snd_seq                67728   4 snd_seq_oss,snd_seq_midi_event
snd_seq_device         8328   2 snd_seq_oss,snd_seq
.
.
.
aufs                 16512   0
ne2k_pci              9056   0
8390                 13568   1 ne2k_pci
oncl1394              41660   0
fee1394               28464   1 ohci1394
floppy                 65712   0
sg                     36120   0
scsi_mod              124600   1 sg
parport_pc             39724   0
parport                47336   1 parport_pc
ext3                  128424   2
jbd                   86040   1 ext3
```
```

This output shows a variety of modules that have been loaded on a Linux system. The modules loaded on this system include several to support sound, including some that provide OSS compatibility (snd_seq_oss).

To find information about any of the loaded modules, you can use the `modinfo` command. For example, you could type the following:

```
```
# modinfo snd-seq-oss
filename:	/lib/modules/2.6.18-128.el5/kernel/sound/core/seq/oss/
```
```