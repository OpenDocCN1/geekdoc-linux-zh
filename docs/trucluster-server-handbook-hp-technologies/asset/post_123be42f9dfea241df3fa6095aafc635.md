
The 'roll' stage has completed successfully. This member must be rebooted in order to run with the newly installed software.
Do you want to reboot this member at this time? [ ]: yes
You indicated that you want to reboot this member at this time.
Is that correct? [yes]: yes
The 'roll' stage of the upgrade has completed successfully.

As soon as the cluster member finishes rebooting, it configures the individual software subset for member 2.

After the configuration of all the software subsets is complete, a new kernel will be built for this cluster member. The new kernel will be copied in place, and the system is rebooted.

```
Saving /sys/conf/SHERIDAN as /sys/conf/SHERIDAN.bck
The system will now automatically build a kernel
with the selected options and then reboot. This can take
up to 15 minutes, depending on the processor type.
*** PERFORMING KERNEL BUILD ***
...
System rebooting
```

This cluster member is now running on the new TruCluster Server software.

## 25.5.6.2 Rolling a Cluster Member after the dupatch Program

The output of a roll of a cluster member after a Patch Kit Installation is much simpler than a roll after an Update Installation.

```
# clu_upgrade roll

This is the cluster upgrade program.
You have indicated that you want to perform the 'roll' stage of the upgrade.
Do you want to continue to upgrade the cluster? [yes]: yes
```

```
Backing up member-specific data for member: 2
...
The 'roll' stage has completed successfully. This member must be rebooted in order to run with the newly installed software.
Do you want to reboot this member at this time? [ ]: yes
```

```
You indicated that you want to reboot this member at this time.
Is that correct? [yes]: yes
```

After the cluster node is rebooted, the newly patched software subsets are installed and configured. Finally a new kernel is built and copied into place. The cluster member is again rebooted, but this time, when the system comes back up it will do so on the newly patched TruCluster Server software.

## 25.5.6.3 A Final Word on Rolling Cluster Members

The Roll Stage is not complete until each and every cluster member, except the lead cluster member, is rolled. If a cluster member goes down and cannot be rebooted before all cluster members are rolled, it is recommended that this cluster member be deleted from the cluster. You can always add this cluster member back after the Rolling Cluster Upgrade is complete and this system is repaired.

## 25.5.7 Switch Stage

The Switch Stage is where we actually turn on any new software features installed during the Install Stage. Until this point, after the Install Stage and prior to the completion of the Roll Stage, the cluster was actually operating on two different versions of the operation system and TruCluster Server software. One of the ways it does this is by making sure that active features between the different versions of the software are as compatible as possible. This is handled by effectively "turning off" or disabling any and all new features installed during the Roll Stage until the entire cluster is at the same version of the software.

In detail, let's see what happens when the "clu_upgrade switch" command is executed:

- First, it verifies that all cluster members have been rolled and that they are all operating off the same version of the operating system and the TruCluster Server software.
- The new version ID of the operating system and cluster software is then set in each cluster member's /etc/sysconfigtab file. This version ID corresponds to the running kernel.

This "clu_upgrade switch" command is executed in multi-user mode and on any cluster member. This command is only executed once and only on one node of the cluster.

```
# clu_upgrade switch
This is the cluster upgrade program.
You have indicated that you want to perform the 'switch' stage of the upgrade.
Do you want to continue to upgrade the cluster? [yes]: yes
```

```
Initiating version switch on cluster members
"
The cluster upgrade 'switch' stage has completed successfully.
All cluster members must be rebooted before running the 'clean' command.
```

After the "clu_upgrade switch" command completes, every member in the cluster must be rebooted one at a time. For the convenience of the System Administrator and the users, the reboot of each cluster member can be done over time.

# CAUTION:

It should be noted that as soon as the Switch Stage is completed or the "switch thrown," you cannot issue any "clu_upgrade undo" commands.
