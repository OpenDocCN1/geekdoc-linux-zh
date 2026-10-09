Linux has several different programs for backing up and restoring data. A backup program is needed to do the actual operation, but a backup policy is needed to document how, what, and when to back up.

# fsck Command

Disk drives will have errors. Most drives are rated to perform up to a specific number of hours, and thereafter failures can be expected. A hard disk is a delicate device, assembled in an industrial clean room under ideal conditions. If even one smoke particle gets into the drive, it can cause a head crash. A head crash occurs when the read/write head bumps into the metal platters of the disk, which are often spinning at over 7200 rpm. Catastrophic failures can be fixed only by replacing the hard drives and restoring the information from backup; however, often the errors are minor and may affect only a few files. Utilities can scan for damaged areas of the hard drive, the files can be moved to other areas, and the bad sectors can be marked. The fsck program is used to check and optionally repair one or more Linux file systems. The syntax for fsck is **fsck [ -options ] [ file system ]**. The file system to be checked should be unmounted first. If areas that require corrective action are found, you are prompted for a yes or no to correct the file system. The default answer is no. If you answer yes, the default for the next prompt will be yes. If you use the -y option, the default answer to all fsck questions is yes. An example listing follows:

```
# cat /etc/fstab
LABEL=/                     /                  ext3    defaults           1 1
LABEL=/boot                 /boot              ext3    defaults           1 2
none                        /dev/pts           devpts  gid=5,mode=620     0 0
/dev/hda3                   /newDrive          ext3    defaults,usrquota  1 2
none                        /proc              proc    defaults           0 0
none                        /dev/shm           tmpfs   defaults           0 0
/dev/hda5                   swap               swap    defaults           0 0
/dev/cdrom                  /mnt/cdrom         udf,iso9660 noauto,owner,kudzu,ro 0 0
/dev/fd0                    /mnt/floppy        auto  noauto,owner,kudzu   0 0
/dev/cdrom1                 /mnt/cdrom1        udf,iso9660 noauto,owner,kudzu,ro 0 0
# umount /newDrive
# fsck /newDrive
fsck 1.32 (09-Nov-2002)
e2fsck 1.32 (09-Nov-2002)
/dev/hda3: clean, 33/375360 files, 47132/750330 blocks
# mount -a
# cd /newDrive
# ls
dengle jsmith ksmith lost+found quota.user rbrown
# cd /
#
```

If the Linux operating system is suddenly powered off, file systems with open files have a high chance of being damaged. If that is the case, you will be prompted to run fsck during the next startup and a command prompt will be made available. Follow the onscreen instructions. When fsck repairs a file system, lost files may sometimes be found in the lost + found directory. One way to avoid a damaged file system is to use an uninterruptible power supply (UPS). A UPS is a battery that provides power to the computer system if main power is lost. Some UPSs have software that will communicate with the computer system to determine the battery status and shut down the system if necessary.

# Configuration File Problems

Many programs in the Linux operating system are controlled by configuration files. The configuration files are used for everything from user profile information to information on how to mount file systems. Most of these programs were discussed in Chapter 8.