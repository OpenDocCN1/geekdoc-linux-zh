
You should hear your Zip drive activate for a short time. You can then use the `dmesg` command to see what happened:

```
# dmesg
```

```
ppa: Version 2.03 (for Linux 2.2.x)
ppa: Found device at ID 6, Attempting to use EPP 32 bit
ppa: Communication established with ID 6 using EPP 32 bit
scsi0 : Imagen VPD0 (ppa) interface
scsi : 1 host.
  Vendor: IBM       Model: ZIP 100        Rev: D.17
  Type:   Direct-Access                     ANSI SCSI revision: 02
Detected scsi removable disk sda at scsi0, channel 0, id 6, lun 0
SCSI device sda: hwr sector= 512 bytes. Sectors= 196608 [96 MB] [0.1 GB]
sda: Write Protect is off
  rda: sda4
```

As you can see, Linux recognized the drive as a SCSI device (attached to your notebook's parallel port). The SCSI device recognized is /dev/sda4. You can then mount the Zip disk at a desired mount point (such as /mnt/zip) with the `mount` command:

```
# mount -t vfat /dev/sda4 /mnt/zip
```

You can verify the disk using the `df` command:

```
# df /mnt/zip
```

| Filesystem | Size | Used | Avail | Use% | Mounted on |
|---|---|---|---|---|---|
| /dev/sda4 | 96M | 84M | 11M | 88% | /mnt/zip |

As you can see, this particular disk (which uses the vfat filesystem) is nearly full. If you use the `umount` command to unmount the Zip disk, you can then use Linux utilities such as `mke2fs` to reformat the Zip disk as a native Linux partition. These disks are an inexpensive way to store archives, backups, or other information, and they can be used like any other hard drive while mounted. Linux also comes with the `mzip` command, which may be used to query, eject, or password- or write- protect your Zip disk. You can also use the jaZip client for X11 (shown in Figure 12.5) to query, mount, unmount, lock, and unlock Zip disks. Download the program, build the software, and then start the program with this command:

```
# jazip &
```

Convenient buttons are used to control your Zip disk, and a scrolling display provides status messages.

![](img/70d85e6f4d1ff2750ca2a98ba3d9855c_315_0.png)

Figure 12.5 The jaZip X11 client can be used to mount, unmount, query, lock, and unlock Iomega Zip disks with Linux.

## Resource Information

- [http://samba.anu.edu.au/rsync/](http://samba.anu.edu.au/rsync/)
    - The rsync home page, where you'll find the latest version, along with examples.
- [ftp://trycham.ce.ryerson.ca/pub/PalmOS/](ftp://trycham.ce.ryerson.ca/pub/PalmOS/)
    - The repository for the latest version of the pilot-xfer software (in the pilot-link package), along with the Linux m68k cross-compiler and information needed to build Palm PDA clients for Linux.
- [http://www.s1ac.com/pilone/kpilot_home/mainpage.html](http://www.s1ac.com/pilone/kpilot_home/mainpage.html)
    - The home page for the KPilot software for KDE and Palm PDA users. Browse to download the latest version or to get more information about this program.
- [http://www.torque.net/~/campbell/](http://www.torque.net/~/campbell/)
    - Dave Campbell's Zip drive Web pages, with loads of information on using legacy and newer Zip drives with Linux, along with links for downloading the very latest drivers.
- [http://www.linuxdoc.org/HOWTO/mini/ZIP-Drive.html](http://www.linuxdoc.org/HOWTO/mini/ZIP-Drive.html)
    - Kyle Dantis's Zip Drive Mini-HOWTO. Required reading for using Zip drives with Linux.
- [http://www.scripps.edu/~-jsmith/jazip/](http://www.scripps.edu/~-jsmith/jazip/)
    - Home of the jaZip graphical Zip and Jaz drive software.

Just because you're away from the office doesn't mean you're stranded when you run into problems. Learn how to exercise some preventive maintenance and recover gracefully from errors or problems that would leave other users high and dry or up the proverbial creek without a paddle. You'll see how to restore data, maneuver around printing problems, connect to the Internet while on the road, keep track of time, and save battery power. You'll also get an introduction to some classy and classic pastimes while you're off-line or have down time.

- 13 Crash Prevention and Recovery
- 14 Printing on the Road
- 15 Getting Connected on the Road
- 16 Time Zones and Locales
- 17 Battery Power
- 18 On-the-Road Entertainment
- 19 The Essential Road Kit

# PART III

On the Road—Problems and Solutions

![](img/70d85e6f4d1ff2750ca2a98ba3d9855c_316_0.png)

# Chapter 13: Crash Prevention and Recovery

- 1. Preventive Tips
- 2. Backup Strategies
- 3. Backup Devices
- 4. Backup Software
- 5. Alternative Backup Methods
- 6. Hard Drive Maintenance On-the-Fly
- 7. Restoring Your Hard Drive
- 8. Resource Information

![](img/70d85e6f4d1ff2750ca2a98ba3d9855c_318_0.png)

The best way to make sure your data is safe is to take preventive steps before a tragedy. This means that you should always expect that disaster will strike. Hard drive crashes and data loss can occur for a number of reasons, and mobile Linux users face additional hazards. Here are some of the things that can happen:

- Your notebook is stolen (several hundred thousand are stolen each year).
- You drop your notebook.
- A soft drink is spilled on your notebook’s keyboard.
- Someone hacks into your notebook and changes the BIOS startup and hard drive password.
- You leave your notebook online, and someone breaks into your system.
- A critical component, such as the display, keyboard, or hard drive, fails.
- You accidentally delete critical files or your entire filesystem.
- A software installation renders your LILO boot loader inoperable and unable to boot Linux.

I’m sure there are many other horror stories of what can happen to a notebook (or other device, such as a friend’s Palm PDA that became a crunchy dog toy; thank heavens the Palm LCDs are covered by a plastic coating). This chapter outlines some basic steps you can take to prevent catastrophic loss of data or use of your notebook. Some of the techniques are just common sense, and others might help you recover from a problem when installing, updating, or upgrading Linux or other software.

### Preventive Tips

When you first get your notebook, write down its serial number and store it in a safe place. Many online or mail-order shippers and manufacturers also include the notebook’s serial number on the sales receipt or on the shipping box. You’ll generally find the serial number on the bottom of your notebook, most likely on the FCC plate.

Make sure your notebook is insured. If you live in an apartment, get replacement-cost insurance. Your homeowner’s insurance might cover your notebook, but if it is used for business, you might need a special rider. If your company provides your notebook, check on policies regarding theft or misuse. If you use your own notebook at work or for work, check on policies regarding replacement of personal equipment.

You can deter thieves or disreputable pawn shops by permanently defacing your notebook with an engraving pen or epoxied sticker with your personal information.

### Use the BIOS

One of the first things you should do is set the BIOS password, system password, or hard drive password. Reboot your computer, and then press the required *F1* or other key combination needed to bring up the BIOS configuration screen. Most BIOS menus offer the choice of startup, return from suspend, and BIOS change password settings. Use all password settings, and use different passwords for different settings.

Setting BIOS passwords renders most notebooks useless to the casual thief or potential buyer. However, there are ways to circumvent set BIOS passwords. Some manufacturers even offer technical and hardware manuals on the Web with detailed information on how to defeat set passwords. For example, to reset a BIOS password on the 1400 series of IBM ThinkPads, you do the following:

1. Turn off and unplug the notebook, and remove the battery.
2. Remove the keyboard.
3. Remove a thermal plate.
4. Move SW2 (switch 2), the password switch, from off to on.
5. Plug in the AC adapter, and boot the notebook.
6. Press F1 to enter the BIOS (after the beep).
7. Select System Security, and then set the Power-on Password to None.
8. Save the BIOS settings.
9. Shut down and unplug the notebook.
10. Move the password switch from on to off.
11. Reassemble the notebook.

Disabling the BIOS power-on password on the 390 or 1700 series ThinkPads is even easier:

1. Unplug the notebook, and remove its battery.
2. Remove the notebook's backup battery for 20 minutes.
3. Alternatively, short out the backup battery for one second.
