# Appendix F: Kickstart Installations

then you will need to have both of these specified in the configuration file and you will need to have --continue after the first one in the configuration file:

```
device scsi aic7xxx --continue
device scsi
BusLogic
```

However, if you have multiple adapters of the same type, then you will not need to be concerned with this line, as the single module insertion is enough to control all adapters of that type. For example, if you have three Adaptec adapters, then the single line

```
device scsi aic7xxx
```

will load and allow all three adapters to function.

# Partitioning

The hard drive in the machine must be partitioned before Red Hat Linux can be installed. In this section, we will describe how to specify disk partitioning in the kickstart file.

# zerombr — Partition table initialization

First, if you are installing Red Hat Linux on a new machine, you should use the zerombr keyword to clear the current partition information. This is a good idea, because the partition table on new hard drives is usually bogus. Here's an example of zerombr on a new system:

```
zerombr yes
```

On the other hand, if you are installing machines that have a valid partition table, even if you want to change part (or all) of it, you should use zerombr this way:

```
zerombr no
```