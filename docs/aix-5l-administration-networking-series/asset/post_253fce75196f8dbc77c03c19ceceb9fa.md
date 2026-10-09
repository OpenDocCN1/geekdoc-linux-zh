
## Device Names

Along with the block size, you must also be aware of the implicit tape I/OCTL operations associated with the device special filenames. Device special filenames are associated with a unique major number that identifies the tape device, driver location in the device switch table. A per-device unique minor number identifies entry points in the tape device driver that correspond to various density and tape control operations. If you are familiar with other UNIX tape systems, you know that nearly everyone uses his or her own scheme for naming device special files. Table 10-2 represents the AIX default device names and the corresponding control operations and densities.

| VENDOR | HINT |
|---|---|
| DEC | OK. Check for compatible tape type/density. |
| Sun | Sun uses 512-byte blocks by default. On RS/6000, set block size to 512 or use dd conv=sync to pad blocks when reading Sun tapes. |
| HP | OK. Check for compatible tape type/density. |
| SGI | Swap byte pairs using dd conv=swab. |

Table 10-1. RS/6000 and pSeries Tape Conversions Using tar

The high and low density values are dependent upon the device. Consult the vendor documentation concerning the device characteristics.

Make sure you take a close look at the rmt man page information on how BOT, EOF, and EOT are handled for both reading and writing. You may be in for a surprise if you do not select the correct device name for your application’s requirements. This can be especially true for EOT handling on nine-track tape drives. UNIX generally does not sense EOT before reaching it. Improper tape positioning at EOT can cause the application to run the tape off the end of the reel. You will make few friends in the operations staff if you do this very often.

| FILENAME | REWIND ON CLOSE | RETENTION ON OPEN | DENSITY |
|---|---|---|---|
| /dev/rmt*.* | Yes | No | High |
| /dev/rmt*.1 | No | No | High |
| /dev/rmt*.2 | Yes | Yes | High |
| /dev/rmt*.3 | No | Yes | High |
| /dev/rmt*.4 | Yes | No | Low |
| /dev/rmt*.5 | No | No | Low |
| /dev/rmt*.6 | Yes | Yes | Low |
| /dev/rmt*.7 | No | Yes | Low |

Table 10-2. Tape Device Name Implicit Options

## Tape Positioning

The tape device driver supports a somewhat standard set of **ioctl** operations used to control tape positioning. These operations can be invoked from the local command line, remotely, or within a program. Local and remote positioning is handled by the **tctl** and **mt** commands, respectively. If you are familiar with the **mt** command on other UNIX platforms, both **mt** and **tctl** are now supported by the same hard-linked runtime, as can be seen by executing the command **what /usr/bin/mt**.

```
# tctl -f /dev/rmt0 rewind                    Rewind the rmt0 tape drive
# tctl -f /dev/rmt0 offline                   Rewind and eject the rmt0 tape drive
# mt -f /dev/rmt0 rewind                       Rewind the rmt0 tape drive
# mt -f /dev/rmt0 offline                      Rewind and eject the rmt0 tape drive
```

For remote operation, be aware that AIX **ioctl** call numbers don’t necessarily map one-for-one with those on the remote system (see Table 10-3). You can fix the mapping problem by creating a wrapper for **mt** to remap the command-line parameters to those in use by the remote system.

| AIX | ioctl Number | Remote | ioctl Number | Comment |
| --- | --- | --- | --- | --- |
| STOFFL | 5 | MTOFFL | 6 | Rewind unload tape |
| STREW | 6 | MTREW | 5 | Rewind tape |
| STERASE | 7 | MTERASE | 9 | Erase tape |
| STRETEEN | 8 | MTRETEEN | 8 | Rerention tape |
| STWEOF | 10 | MTWEOF | 0 | Write end-of-file marker |
| STFSF | 11 | MTFSF | 1 | Forward space file |
| STRSF | 12 | MTBSF | 2 | Back space file |
| STFSR | 13 | MTFSR | 3 | Forward space record |
| STRSR | 14 | MTBSR | 4 | Back space record |
| N/A | N/A | MTNOP | 7 | NO-OP |
| N/A | N/A | MTEOM | 10 | End-of-media |
| N/A | N/A | MTNBSF | 11 | Back space to BOF |

Table 10-3. AIX to UNIX ioctl Mapping

Be aware of where you are during tape operations. After each program **read()** or **write()** operation, the tape head is positioned at the beginning of the next block or the beginning of blank space. Tape marks are treated exactly like a file, so they must be accounted for when skipping from file to file on a tape.

## Permissions

Restricting access to tape devices tends to be a problem on many UNIX systems. The device special files are commonly set **read/write** by the world. In the absence of additional tape allocation software, you can easily create your own drive reservation application using the following algorithm:

1.  Check for a free device (absence of device lock files). If all devices are in use, exit. If not, continue.
2.  Fork and spawn a new shell. Wait until process exit to release the device.
3.  Create a lock file for the selected device.
4.  Set permissions and ownership to the requester.

The following are the default device permissions:

```
# ls -1 /dev/rmt*

crw-rw-rw- 1 root system 19, 0 Feb 17 23:58 /dev/rmt0
crw-rw-rw- 1 root system 19, 1 Feb 17 22:58 /dev/rmt0.1
crw-rw-rw- 1 root system 19, 2 Jul 26 2001 /dev/rmt0.2
crw-rw-rw- 1 root system 19, 3 Jul 26 2001 /dev/rmt0.3
crw-rw-rw- 1 root system 19, 4 Jul 26 2001 /dev/rmt0.4
crw-rw-rw- 1 root system 19, 5 Jul 26 2001 /dev/rmt0.5
crw-rw-rw- 1 root system 19, 6 Jul 26 2001 /dev/rmt0.6
crw-rw-rw- 1 root system 19, 7 Jul 26 2001 /dev/rmt0.7
```

## TAPE TOOLS

AIX provides a limited set of tape utilities. The following set of commands supports tape manipulation:

- **dd** Read/write variable block sizes and perform data conversion
- **tcopy** Display tape directory or copy tape to tape
- **tar, cpio, pax, backup/restore** Archive; may use tape as a media
- **rdump, zrestore** Remote archive and restore; may use tape as a media

## LINEAR OPEN TAPE (LTO) ULTRIUM TAPE DRIVES

In 1997, a consortium was formed between IBM, HP, and Seagate for a new open tape standard. Ultranium is the first LTO offering from IBM. With Ultranium LTO, you get high capacity at 100GB per tape and high performance at 10–20 MB/second.

The LTO tape drive uses an open industry standard and has improved reliability over DLT, improved capacity (by 250 percent) over DLT, and improved performance (by 250 percent) over DLT. Since LTO is an open format, there are multiple manufacturers of media and drives, and the cartridges are interchangeable. There are four generations in the works for LTO Ultrium tape drives as shown in Table 10-4.

For a complete list of all of the tape cartridge, tape drives, and tape library specifications, refer to the IBM Web site at `http://www.storage.ibm.com/ssg.html`. From this Web page, select the TotalStorage Solutions product guide to view the PDF file.

**IBM’s Four LTO Ultrium Options**

- Ultrium Tape Drive—Models 3580-L11 and 3580-H11
- Ultrium Tape Autoloader—Models 3581-L17 and 3581-H17
- Ultrium Scalable Tape Library—Model 3583
- UltraScalable Tape Library—Model 3584 L32 or D32

You can get more information on each of these IBM offerings at `http://www.ibm.com/storage/lto`.

New to the LTO Ultrium Scalable Tape Library and the UltraScalable Tape Library is the capacity for Native Fibre Channel connectivity through the internal SAN Data Gateway Module.

At the high end of the Ultranium LTO offerings is the IBM UltraScalable Tape Library 3584-L32. This machine uses an exclusive multipathing architecture with up to 12 logical library partitions, supports both Native Fibre Channel and SCSI LTO drives, is autocalibrating, has Dual Picker Robotics, supports redundant power supplies, and can hold 141 to 281 Ultrium tape cartridges.

The LTO Ultrium Scalable Tape Library supports enhanced management capabilities using StorWatch Expert ETL, which is a different StorWatch product than the version used on the Enterprise Storage Server (ESS, a.k.a. the Shark). StorWatch Expert ETL provides remote management capability by way of your Web browser, which allows all of the operator control panel functions to be handled through the network, including microcode downloads. This functionality also allows for SNMP monitoring of the tape library.

The following operating systems are supported for LTO Ultrium attachments:

- AIX 4.3.2 or later
- OS/400 V4R4 or later
- Microsoft Windows NT 4.0 with service pack 6
- Microsoft Windows 2000 for build 2195 or later
- Sun Solaris 2.6, Solaris 7, and Solaris 8
- HP-UX 11.0

Most backup software is supported in the LTO Ultrium tape systems, but Tivoli Storage Manager (TSM) is preferred by IBM.

## IBM 3494 ENTERPRISE TAPE LIBRARY

The IBM 3494 Enterprise Tape Library is the workhorse for backup and recovery in many large enterprises. The 3494 can store over 6000 tape cartridges and supports up to 76 Magstar tape drives. The nice thing about the 3494 Tape Library is that it is expandable to up to 16 library frames, which can store up to 748TB of stored data.

The Tape Library Base Frame holds the brains of the 3494 tape subsystem. The control mechanism is a PC running OS/2, which runs the tape and robotic subsystems. Each Tape Library Base Frame consists of the Tape subsystem, which supports IBM 3590 and 3490E tape libraries, the Library Manager, a single- or dual-gripper tape cartridge accessor, cartridge storage cells, which run across the front and back of the frame, and an optional I/O station.

There are three types of expansion frame options to extend the capacity of the 3494 Tape Library:

- **Tape drive expansion frames** This type of frame is used to provide additional tape drives and cartridge cells. Three types of drive frames allow for flexibility in choosing the tape drive technology to suit your particular needs.
