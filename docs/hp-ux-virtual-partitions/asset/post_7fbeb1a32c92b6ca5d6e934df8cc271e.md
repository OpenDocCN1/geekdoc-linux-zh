
![](img/eff8b9287a5f38c5adf538f24aacf29e_633_0.png)

Figure 11-4 SAM Showing Virtual Console-Related Drivers

Chapter 4 covers many aspects of performing vPar kernel-related work at the command line. All of this kernel-related work can also be performed in SAM. The background portion of this chapter covers many aspects of kernel-related work in SAM.

## Backup Using SAM

Chapter 7 covered backup and Virtual Partitions. Much of the work done in Chapter 7 was at the command line. Backup can also be managed through SAM. This backup section is from Chapter 7, but I’ve included it here to save you the trouble of flipping to Chapter 7. Let’s take a look at the SAM backup functional area for two vPars - *cable1* and *cable2*. A substantial amount of work was done at the command line to perform a backup of these two vPars in Chapter 7. This same backup can be achieved using SAM. This includes the backup of cable2 to the remote tape drive on cable1. Although cable1 and cable2 are on the same computer system the tape drive connected to cable1 is considered remote to cable2 since there are two different vPars.

Let's first perform a backup of cable1 using Backup and Recovery - Interactive Backup and Recovery in SAM. Figure 11-5 is a full CDE screen shot showing some of the SAM windows related to Interactive Backup and Recovery for cable1:

![](img/eff8b9287a5f38c5adf538f24aacf29e_634_0.png)

All of the SAM windows in Figure 11-5 have in the top of them the hostname of cvhdccon3, which is the hostname for cable1. The top-left window shows that the DDS drive that was configured as part of the cable1 vPar is selected as the backup devices. The bottom-right windows is the one in which we can specify the backup scope.

Performing this interactive backup of *cable1* could not be simpler with SAM. Let’s now see if we can backup *cable2* to the remote tape drive on *cable1*. Keep in mind that as far as SAM is concerned, these are two completely different systems, even though vPar *cable1* and *cable2* are running on the same computer. This means that the backup of *cable2* to the tape drive on *cable1* is remote.

We can initiate the backup of *cable2* in two different ways. The first would be to invoke SAM on *cable2* and specify all of the appropriate information. The second is to run SAM remotely. We’ll chose the latter approach. We first specify from *cable1* the name of the remote system on which we want to run SAM, as shown in Figure 11-6:

![](img/eff8b9287a5f38c5adf538f24aacf29e_635_0.png)

Figure 11-6 Add vPar *cable2* as a Remote System on Which to Run SAM

After we specify the hostname of *cvhdcn4* and make a note that this is vPar *cable2*, we press OK and SAM configures this as a remote host.

We can now run select the remote host and run SAM on it as shown in Figure 11-7:

![](img/eff8b9287a5f38c5adf538f24aacf29e_636_0.png)

Figure 11-7 Configure Remote Tape Device on *cable1* for Backup of *cable2*

All of the SAM windows in Figure 11-7 now show a hostname of *cvhdcn4*, which is the remote hostname for *cable2*. The top-right window shows that we have selected **vPar cable2** (hostname *cvhdcn4*) as the remote system on which to run SAM. The bottom-right window shows that we have selected **/dev/rmt/0m** on *cvhdcn3* (the hostname for **vPar cable1**) as the device on which the backup will take place.

We have now performed all of the setup required to proceed with the backup to the remote tape drive. After selecting **/var/tmp** as the directory to backup SAM opened, the window shown in Figure 11-8 indicated that the backup of **/var/tmp** is taking place:

![](img/eff8b9287a5f38c5adf538f24aacf29e_637_0.png)

**Figure 11-8** *Interactive Backup and Recovery for cable1*

This backup completed with no problems.

This backup work of two different vPars on the same computers demonstrates the kind of isolation that vPars provide. The work we perform in one vPar does not affect the other vPar. To use a tape drive on the same computer but in a different vPar requires us to specify the tape drive as a remote device. If you’re accustomed to using SAM to perform your local and remote backups, you can continue to use SAM in your vPars environments as long as you treat different vPars as separate systems from the perspective of SAM.

## Users and SAM

Chapter 6 covered users and Virtual Partitions. This is the part of Chapter 6 that covers users and SAM. I've included it here to save you the trouble of flipping to Chapter 6. Let's now create a new user on each of the two vPars called **cable1** and **cable2**. On **cable1** we'll create the user **cable1us** and verify that this user does not exist on **cable2**. On **cable2** we'll create the user **cable2us** and verify that this user does not exist on **cable1**. See the background portion of this chapter for detailed information on creating users.

Figure 11-9 shows a System Administration Manager (SAM) screen shot of creating a user **cable1us** in vPar **cable1**.

![](img/eff8b9287a5f38c5adf538f24aacf29e_638_0.png)

**Figure 11-9** Creating **cable1us** in SAM

The user *cable1us* was created in *vPar cable1* and exists only in *cable1*. We’ll verify this shortly. We performed the same procedure creating user *cable2us* in *vPar cable2* using SAM.

There should now be one user in *cable1* that is not viewable in *cable2*, and vice versa. The following shows connecting to *cable1* and listing the contents of */etc/passwd*.

```
cvhdecon3: # cat /etc/passwd
root:hiIXKaZUIFy6:0:3::/:/sbin/sh
daemon:*:1:5::/:/sbin/sh
bin:*:2:2::/usr/bin:/sbin/sh
sys:*:3:3::/
adm:*:4:4::/var/adm:/sbin/sh
uucp:*:5:3::/var/spool/uucppublic:/usr/sbin/uucp/uucico
lp:*:9:7::/var/spool/lp:/sbin/sh
nuucp:*:11:11::/var/spool/uucppublic:/usr/sbin/uucp/uucico
hpdb:*:27:1:ALLBASE::/:/sbin/sh
nobody:*:-2:-2::/
www:*:30:1::/
webadmin:*:40:1::/usr/obam/server/nologindir:/usr/bin/false
smbnull:*:101:101:DO NOT USE or DELETE - needed by Samba: /home/smbnull:/sbin/sh
cpc_op:*:777:77::OPC default operator::/home/opc_op:/usr/bin/ksh
cable1us:102:20::/:/home/cable1us:/usr/bin/sh
cvhdecon3: #
```

This listing for *cable1* shows that *cable1us* exists in the */etc/passwd* file on *cable1*, however, there is no *cable2us* present in this file.

The following shows connecting to *cable2* and listing the contents of */etc/passwd*.

```
# cat /etc/passwd
root:Jx66ARmhj.aBs:0:3::/:/sbin/sh
daemon:*:1:5::/:/sbin/sh
bin:*:2:2::/usr/bin:/sbin/sh
sys:*:3:3::/
adm:*:4:4::/var/adm:/sbin/sh
uucp:*:5:3::/var/spool/uucppublic:/usr/sbin/uucp/uucico
lp:*:9:7::/var/spool/lp:/sbin/sh
nuucp:*:11:11::/var/spool/uucppublic:/usr/sbin/uucp/uucico
hpdb:*:27:1:ALLBASE::/:/sbin/sh
nobody:*:-2:-2::/
www:*:30:1::/
webadmin:*:40:1::/usr/obam/server/nologindir:/usr/bin/false
sam_exec:xxx:0:1:/home/sam_exec:/usr/bin/sh
cable2us::101:20::/home/cable2us:/usr/bin/sh
# 
```

This listing for `cable2` shows that `cable2us` exists in the `/etc/passwd` file on `cable2`, however, there is no `cable1us` present in this file.

This listing shows that unique users for the respective vPars exist only on the vPar on which they were created. In addition, each vPar has its own `root` and other system-level users.

## ServiceControl Manager (SCM) and Virtual Partitions

SCM allows you to replicate tasks over multiple systems. Tasks that have traditionally been performed individually on many systems can now be performed across multiple systems in a cluster managed by SCM. This is particularly relevant to Virtual Partitions since you have one computer system with more than one Virtual Partition running on it. In most cases you’ll want to have SCM control of these Virtual Partitions since they’re running on the same computer system even though you have multiple instances of HP-UX.

You can take a command or tool that runs on an individual system, such as the `find` or `df` command, dispatch it to run on multiple systems or Virtual Partitions, and collect the results for review in SCM.

More advanced tools that were designed to run on multiple systems, such as Ignite-UX, can also be run in the same manner using SCM.

Specific tasks can be assigned to specific individuals with SCM, thus creating a role-based environment. This obviates the need for root access to systems because specific management activities are assigned to specific users on specific nodes. These user roles provide great flexibility in defining the tasks that individual users can perform.

You can define the systems and/or Virtual Partitions of which an SCM cluster is composed. The Central Management Server (CMS) in an SCM environment is the focal point in which management takes place. Agents on the managed nodes communicate with CMS to perform management functions. The CMS could be one of your Virtual Partitions.
