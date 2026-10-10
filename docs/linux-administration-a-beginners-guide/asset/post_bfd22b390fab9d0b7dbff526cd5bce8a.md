
being compressed. Textual data for example, compresses very well. Certain graphics or sound formats get little to no compression at all. When you estimate the amount of data you can store on a single unit, be sure to consider the mix of data on your servers.

Another aspect of hardware to consider is your tape drive and its relationship to the backup server. Will the tape drive be in contention with other peripherals on the system?

For instance, will the tape drive be on the same SCSI chain as a disk that’s being backed up? And finally, are you able to feed data to the tape drive fast enough so that it can stream? If the tape drive cannot stream, it will stop writing until it gets more data. This pause may be as long as several seconds on a slow meansystem, while the drive realigns itself, when the tape and finds the next available position to write data. Even if the pause is brief, when it occurs thousands of times during a single backup run it can increase your backup runtimes by many hours.

## How Much Network Throughput?

Network throughput is, unfortunately, easily forgotten in the planning of backup operations. But what good do you get from a really fast backup server and tape drive if you feed the data in through a thin straw?

Take the necessary time to understand your network infrastructure. Look at where the data is coming from and where it’s going. Use SNMP tools, such as MRTG (http://www.mrtg.org), to collect statistics about your switches and routers. If you need to back up machines that are connected via hubs, consider a backup sequencer that won’t back up two machines on the same collision domain at the same time.

Gathering all this information will help you estimate the bandwidth necessary to perform backups. With your analysis done, you’ll be able to figure out which upgrades will net you the best return for your money.

## What Kind of Recovery?

When requests to restore data from tape arrive, you’re likely to be under the gun to get the data back to the user as quickly as possible. How long your users have to wait will depend on the tool used for backup. This means you need to incorporate the cost of response time into your backup evaluation. How much are you willing to spend to get the response time you need for a restore. Obviously, faster restores typically mean higher prices.

> **NOTE:** Although this chapter mentions only tape backup, the issues covered here apply to backup on any other media, such as CD-R or even Zip disks. Each medium has its advantages and disadvantages. CD-Rs and Zip disks offer quick access to data, but they lack the high capacity of tape drives. Pick the medium that works best for your system’s needs.

## MANAGING THE BACKUP DEVICE AND FILES

The tape device interacts with Linux just as most other devices do: as a file. The filename will depend on the type of tape drive, your chosen mode of operation (auto-rewind or non-rewind), and how many drives are attached to the system.

SCSI tape drives, for example, use the following naming scheme:

| Device Name | Purpose |
|---|---|
| `/dev/stX` | Auto-rewinding SCSI tape device; X is the number of the tape drive. Numbering of tape drives is in the order of the drives on the SCSI chain. |
| `/dev/ntstX` | Non-rewinding SCSI tape device; X is the number of the tape drive. Numbering of tape drives is in the order of the drives on the SCSI chain. |

Let's say you have a single SCSI tape drive. You can access it using either of these filenames: `/dev/st0` or `/dev/ntst0`. If you use `/dev/st0`, the drive will automatically rewind the tape after each file is written to it. If you use `/dev/ntst0`, on the other hand, you can write a single file to the tape, mark the end of tape, but then stay at the tape's current position. This lets you write multiple files to a single tape.

> **NOTE:** Non-SCSI devices will obviously use a different naming scheme. There is unfortunately no standard for naming backup devices if they are not SCSI devices. The QIC-02 tape controller, for example, uses the `/dev/qtpc*` series of filenames. If you use a non-SCSI tape device (which is a rare thing these days), you will need to find its corresponding driver documentation to see what device name it will use.

> **TIP:** You may find it handy to create a symbolic link from `/dev/stape` to the appropriate device name for the rewinding mode and a link from `/dev/nrtape` for the non-rewinding mode (for example, `/dev/stape` → `/dev/st0` and `/dev/nrtape` → `/dev/ntst0`). This will make it easier to remember the name of the tape device when issuing commands. See Chapter 6 for information on using the `ln` command to create symbolic links.

What makes these backup device files different from disk files is that there is no file-system structure. Files are continuously written to the tape until it's full or until an end-of-tape marker is written. If a tape marker is in non-rewind mode, the write head is left in the position immediately after the last end-of-file marker, ready for the next file to be written.

Think of tape devices as similar to a book, with chapters. The book's binding and the paper, like the tape itself, provide a place to put the words (the files). It's the markings of the publisher (the backup application) that separate the entire book into smaller sub-sections (files). If you (the reader) were an auto-rewinding tape drive, you would close the tape every time you were done with a single file and then have to search through the tape to find the next position (chapter) when you're ready to read it. If, however, you were a non-rewinding tape drive, you would leave the tape open to the last page you read.

## Using mknod to Create the Device Files

If you don't have the file /dev/st0 or /dev/ns0, you can create one using the mknod command. (See Chapter 6 for an explanation of mknod.) The major number for SCSI tape drives is 9, and the minor number dictates which drive and whether it is auto-rewinding or not. The numbers 0 through 15 represent drive numbers 0 through 15, auto-rewinding. The numbers 128 through 143 represent drive numbers 0 through 15, non-rewinding. The tape drive is a character device.

So to create /dev/st0, we would type this mknod command:

```bash
[root@ford /root]# mknod /dev/st0 c 9 0
```

And to create /dev/ns0, we would use this command:

```bash
[root@ford /root]# mknod /dev/ns0 c 9 128
```

## Manipulating the Tape Device with mt

The mt program provides simple controls for the tape drive, such as rewinding the tape, ejecting the tape, or seeking to a particular file on the tape. In the context of backups, mt is most useful as a mechanism for rewinding and seeking.

All of the mt actions are specified on the command line. Table 23-1 shows the parameters for the command.

**Table 23-1. Parameters for the mt Command**

| Parameters for the mt Command | Description |
| :--- | :--- |
| -f tape_device | Specifies the tape device. The first non-rewinding SCSI tape device is /dev/ns0. |
| fcf count | Forward-spaces a number (count) of files. The tape is positioned on the first block of the next file; for example, fcf 1 would leave the head ready to read the second file of the tape. |
| asf count | Positions the tape at the beginning of the file indicated by count. Positioning is done by first rewinding the tape and then spacing forward over count file marks. |
| rewind | Rewinds the tape. |
| erase | Erases the tape. |
| status | Gives the status of the tape. |
| offline | Brings the tape offline and, if applicable, unlodds the tape. |
| load | Loads the tape (applies to tape changers). |
| lock | Locks the drive door (only applies to certain tape drives). |
| unlock | Unlocks the drive door (only applies to certain tape drives). |

> **NOTE:** If you do not use a non-rewinding tape device, the tape drive will automatically rewind after you perform your operation with *it*. This can be rather frustrating if you are trying to seek to a specific file!

**Example** To rewind the tape in `/dev/nst0`:

```
[root@ford /root]# mt -f /dev/nst0 rewind
```

**Example** To move the head so that it is ready to read the third file on the tape:

```
[root@ford /root]# mt -f /dev/nst0 asf 2
```

## COMMAND-LINE TOOLS

Linux comes with several tools that help you perform backups. Though they lack admin-istrative front-ends, they are simple to use and they do the job. Many formal backup packages actually use these utilities as their underlying backup mechanism.

## dump and restore

The *dump* tool works by making a copy of an entire file system. The *restore* tool can then take this copy and pull any and all files from it.

To support incremental backups, *dump* uses the concept of *dump levels*. A dump level 0 means a full backup. Any dump level above zero is an incremental relative to the last time a dump with a lower *dump level* occurred. For example, a dump level of 1 covers all the changes to the file system since the last level 0 dump, a dump level of 2 covers all of the changes to the file system since the last level 1 dump, and so on—covers the way through *dump level 9*.

Consider a case in which you have three levels: the first is a level 0, the second is a level 1, and the third is also a level 1. The first dump is, of course, a full backup. The second dump (level 1) contains all the changes made since the first dump. The third dump (also a level 1) has all the changes *since the first dump*.

The *dump* utility stores all the information about its dumps in the `/etc/dumpdates` file. This file lists each backed up file system, which it was backed up, and at what *dump level*. Given this information, you can determine which tape to use for a restore. For example, if you perform level 0 dumps on Mondays, then level 1 incrementals on Tuesday and Wednesday, and then level 2 increments on Thursday and Friday, a file that was last modified on Tuesday but got accidentally erased on Friday can be restored from Tuesday night's incremental backup. A file that was last modified during the preceding week will be on Monday's level 0 tape.

> **NOTE:** The *dump* tool comes with all distributions of Linux. This utility is file-system dependent, and the version for Linux only works on Linux's native file system (ext2).
