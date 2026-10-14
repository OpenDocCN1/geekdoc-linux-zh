
14. Finally, the newly upgraded TruCluster Server software subsets are installed and loaded.

```
^^^ Load Tru64 UNIX TruCluster(TM) Server Software V5.1A (Rev 1312) Software Subsets ^^^
*** Subsets will be installed.

Loading subset 1 of 3 ...

TruCluster Migration Components
    Copying from /var/adm/update/TruClusterKit (disk)
    Verifying

Loading subset 2 of 3 ...

TruCluster Reference Pages
    Copying from /var/adm/update/TruClusterKit (disk)
    Verifying

Loading subset 3 of 3 ...

TruCluster Base Components
    Copying from /var/adm/update/TruClusterKit (disk)
        Working.... Thu Nov 8 13:09:18 PST 2001
    Verifying
3 of 3 subsets installed successfully.

*** Starting profile merges for Tru64 UNIX TruCluster(TM) Server Software V5.1A (Rev 1312) ***

*** Finished profile merges for Tru64 UNIX TruCluster(TM) Server Software V5.1A (Rev 1312) ***

*** Starting configuration merges for Update Install ***

Update Installation complete with loading of subsets.
Rebooting system with Compute Computer Corporation Tru64 UNIX V5.1A
 generic kernel for configuration phase...

Removing temporary update installation files...done.
***
```

15. The lead cluster member will reboot. When the system comes back up, the software subsets are configured on member0 and then on member1. In this instance, member1 is the designated lead cluster member.

## NOTE:

You may notice that some of the configuration messages are stating that software subsets are being configured on member0. This is only the directory, /cluster/members/member0, on the cluster_root file system and not for cluster member0.

16. After the configuration of all the software subsets, a new kernel will be built for the lead cluster member. The new kernel will be copied in place and the system is again rebooted.

```
...
rebooting.... (transferring to monitor)

...
The system is ready.
```

```
Company T64 UNIX V5.1A (Rev. 1885) (malari.gene.com) console
login: root
Password:

****************************************************************
The 'clu' cluster is currently in a rolled state and the software versions
that are available are different depending on which cluster member you
are on. Additional information about the exact state of the system
can be obtained using the /usr/bin/clu_upgrade command.
****************************************************************
```

17. At this point in the Upgrade Installation, we are just about done with this stage. The next step will be to verify that the Install Stage is complete and successful. See section 25.5.5.1.

## 25.5.4.2 Install Stage for a Patch Kit Installation

We’ve seen the individual steps required to perform the Install Stage for an Update Installation. Now let’s see what it takes to perform the Install Stage of a Patch Kit Installation:

- 1. Update the system firmware on the lead cluster member. Please review the Warning in section 25.5.1.3.
- 2. We are now ready to install the Patch Kit. Again, the following commands must be executed on the lead member:
  - If installing the Patch Kit from multi-user mode:

```
# cd /usr/patch_kit
# ./dpatch
```
← or where your Patch Kit is located

  - If installing the Patch Kit from single-user mode:

```
# shutdown -sb now
# bcheckrc
# reinit start
# cd /usr/patch_kit
# ./dpatch
```
← or where your Patch Kit is located

> **WARNING:**
> 
> While you have a choice of installing Patch Kits in either multi-user or single-user mode, we agree with HP in recommending that the Patch Kit installations should be performed in single-user mode. Doing so will reduce the risk of another Systems Administrator causing unintentional issues.

As the contents of every Patch Kit vary from release to release, we won’t bore you with the details here but instead refer you to the Patch Kit’s Summary and Release Notes for expanded information. It should also be noted that Patch Kits have been known to take anywhere from thirty minutes to two hours to install. This depends on the number of patches in the Patch Kit and the type of server you are attempting to patch.

- 3. Once the dpatch command is complete, reboot the lead cluster member.

## 25.5.5 Postinstall Stage

The Postinstall Stage verifies that the Install Stage has completed and the Update Installation and/or the Patch Kit Installation and/or the NHD Kit Installation has completed successfully. This stage must be done on the "lead" member.

```
# clu_upgrade postinstall
This is the cluster upgrade program.
You have indicated that you want to perform the 'postinstall' stage of the upgrade.
Do you want to continue to upgrade the cluster? [yes]: yes
```

```
The 'postinstall' stage of the upgrade has completed successfully.
```

We would now recommend that you test the newly upgraded software before rolling the other cluster members to this new version.

## 25.5.5.1 Testing the Newly Upgraded TruCluster Server Software

First, let’s test the Cluster File System by relocating a cluster file system between individual cluster members. In this example, we have just completed the installupdate on the server molari. The server sheridan has not been rolled to the new version of the TruCluster Server software yet.

```
# cfsmgr -v -a server /
Domain or filesystem name = /
Server Name = sheridan
Server Status : OK
```

```
# cfsmgr -h sheridan -r -a SERVER=molari /
Recovering filesystem mounted at / to this node (member id 1)
Recovery to this node (member id 1) complete for filesystem mounted at /
```

```
# cfsmgr -v -a server /
Domain or filesystem name = /
Server Name = molari
Server Status : OK
```
