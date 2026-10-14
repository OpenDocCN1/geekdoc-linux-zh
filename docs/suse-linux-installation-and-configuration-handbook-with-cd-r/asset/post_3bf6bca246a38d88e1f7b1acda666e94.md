
8. Now YaST displays all the possible primary partition names that you can have on the drive. Pick the one you want—we recommend that you pick the first one. It should be something like /dev/hdb1.
9. Now it's time to tell YaST how much space this partition should take up. By default, YaST takes all the available space on the drive. You can accept that or tell it the size by writing it in the End of partition field. To specify the size, enter a + before it. For example, 400 MB would be entered as +400M. Press Continue when you are done.
10. YaST shows your new partition table with the newly added partition.
11. Be sure that the new partition is of type Linux Native. You can change it by pressing F3.
12. You can repeat the same process to add more partitions.
13. When you are done, press Continue to have the changes take effect. If you press Abort, you will lose all the changes.

These were the steps for creating a new partition table altogether. If you are simply going to add a new partition that already exists for another operating system, you can use almost the same procedure. All you have to do is follow the same steps and when YaST displays your partition table, find the partition you want to use and change its type to Linux Native, or if you have free unallocated space, create a new partition.

Now that you have the partition all ready to use, you have to format it. This is the easy part. You will use the mkfs (make filesystem) command. To create a second extended filesystem on your new partition—for example, /dev/hdb1—run the command like this:

```
# mkfs -t ext2 /dev/hdb1
```

mkfs takes two parameters, the filesystem type and the partition to format. This will take a short while, and when it is done, your new partition will be ready for use. You now can update your /etc/fstab file and add a new entry for this partition in it.

## Creating a New Swap Partition

To create a new swap partition, you use the exact same procedure as the previous one. You might need to create a new swap partition if your system needs more virtual memory. To do that, simply repeat the previous steps and pick Linux Swap as the partition type. When you format the new partition, use the following command:

```
# mkswap /dev/hda2
```

In your /etc/fstab add a new entry for the new swap partition like this:

/dev/hda2  swap  swap  defaults 0

Be sure that you put the correct device in the entry. To activate the swap partition immediately, use this command:

```
# swapon /dev/hda2
```

That's all. The swap partition will be activated on every boot up automatically.

## Checking Your Filesystem

To maintain your filesystem at top performance, you should check it periodically for errors. Fortunately, the system does that for you after a fixed amount of reboots and when the system shuts down incorrectly. But you might need to check your filesystem manually. How you do so depends on the filesystem you want to check. Please note that you can check only ext2 type partitions. Other types should be checked using their respective operating systems.

To check a partition, you first should unmount it. If this partition is not your root partition, this will be easy. Just follow these steps:

- 1. Unmount the partition with the umount command.
- 2. Run the fsck command:
  `# fsck /dev/device`
- 3. The command will check the filesystem on this device and report any errors found. You then can choose to have it fix them or not.
- 4. When finished, simply mount the partition again and you're done.

To check your root partition, you have to do a little more than this. Follow these steps:

- 1. Switch to single-user mode:
  `# telinit S`
- 2. Remount the root filesystem as read-only:
  `# mount -n -o remount,ro /`
- 3. Check the filesystem using the fsck command:
  `# fsck /`
- 4. When finished, remount the filesystem as read/write:
  `# mount -n -o remount,rw /`
- 5. Switch the system to normal mode:
  `# telinit 3`
- 6. You're done!

When checking partitions, be sure you do not check a filesystem that is mounted read/write. If you can't unmount it then remount it as read/write and then check it. If your system is used by a lot of people, it would be a good idea to switch it to single-user mode before you check the filesystems.

## Understanding the Network Filesystem

So far you have learned how to mount drives that are connected to your machine. Mounting, however, can do a lot more than that. You can even mount drives that exist on remote machines. This is accomplished using the Network Filesystem (NFS). NFS enables you to give others the right to mount your filesystem on their machines across a network.

You might have already used NFS when you installed SuSE Linux. When you install SuSE, you have the option of installing via NFS. This enables you to install from another machine on the network that has a CD-ROM to a machine that does not. The whole process uses NFS to mount the other machine's CD-ROM on your local filesystem and treat it as a part of your machine. All of this happens transparently to you. You don't do anything different from what you would do if you had the CD-ROM on your local machine.

Your machine can be set up to be an NFS client, an NFS server, or both. If you are planning to only mount remote filesystems then you will be interested in being an NFS client only. If you want to allow people to mount your filesystem remotely, you will need to set up your machine as an NFS server.

## Preparing to Use NFS

Before you can start using NFS, you have to configure SuSE Linux for NFS. There are two things you have to configure, the kernel and YaST.

The first thing you want to configure is your kernel. You need to turn on NFS support in the kernel. If you have not modified the kernel that was installed by SuSE, you don't have to worry about this step at all—skip to the next step.

Now you will configure the kernel for NFS. If you are not sure about how to do this, read Chapter 8, "Installing a New Kernel," for more information on the subject. The parameter you want to enable in the kernel is in Filesystems, Network File Systems, NFS Filesystem Support. You can install it either built in or as a module. If you will not be using NFS a lot, we recommend installing it as a module; otherwise, install it built in.

Now your system is configured as an NFS client. This means you can mount remote filesystems. If you are planning to use your own system as an NFS server, you have to configure it to do so using YaST. Follow these steps:

- 1. Run YaST as root.
- 2. Navigate to System Administration, Network Configuration, Configure Network Services.
- 3. YaST will ask you a series of questions. The first one is whether you want to start inetd at boot time. Choose Yes or No. If you want people to be able to telnet or FTP to your machine choose Yes. (This question is not really related to what you are trying to do now, so don't worry about it.)
- 4. The second question is a part of what you want. Should portmap be started at boot time? Choose Yes here because the NFS server needs this to function.
- 5. The third question is should your computer be started as an NFS server? The obvious answer here is Yes. This will allow people to mount your filesystem remotely.
- 6. The last question asks you what you want to have posted in the from line of your new system. Your hostname should be good enough here. Again, this has nothing to do with NFS so don't worry about it.
- 7. That's it. You're all set now to use NFS.

Now that you know how to set up your machine to be both an NFS client and server, it's time to see how to actually use NFS.

## Using NFS (Client-Side)

Using NFS as a client is simple. It is exactly the same idea as mounting local drives. In order to mount a remote filesystem you need to know the name or IP of the NFS server and the name of the directory you want to mount.

The IP of the machine can be substituted with its name on the network. Ask your network administrator for that information if you don't know it. You also should know the name of the directory that you are going to mount. But if you don't, you can use the showmount command to obtain a list of the available directories on the server. To do that, run showmount with the name or IP of the server as a parameter:

```
# showmount -e hostname
```

This will give you a list of all the directories available for remote mounting on this server.

To actually mount a remote directory on your local machine, you issue a mount command. For example, if you are trying to mount a directory called /files on a machine with the IP 192.168.0.25 under /mnt locally, the command would look like this:

```
# mount 192.168.0.25:/files /mnt
```

> TIP
> A good mount option to use is the hard,intr option. This helps in NFS server crashes. Say you are mounting a remote directory, and a program is using a file from that directory. Suddenly, the NFS server on the remote machine crashes, which will cause your program to fail. However, if you supply the mount option with hard,intr, the program will hang for a while until the NFS server is back up and running, then it will continue to do what it was doing. So, the mount command would be as follows:
> # mount 192.168.0.25:/files /mnt -o hard,intr

That's it. Pretty simple, isn't it? And of course, to unmount it, just issue an umount command:

```
# umount /mnt
```
