drive); "hdb1"--second hard drive, first partition (or just "hdb" if it is the CDROM installed as a slave on your first IDE interface), "hdc1"--third hard drive, first partition, etc. SCSI drives have analogous names but start with letters "sd" ("SCSI drive"), followed by the letter indicating the SCSI interface and by number indicating the SCSI device id. For example, "sda" means "first SCSI interface, id number 4". If you have an external zip drive attached to your parallel port, it will appear as a SCSI device "sda4" (it works in a SCSI-emulation mode).

# 1.10 The MS Windows partition occupies my whole harddrive. Can I shrink/split it without a re-install?

Possibly. There is a utility called FEX on your RedHat CD that does just that. Check the directory \dosutils\fipsdoc on your RedHat CD for documentation. If I were, I would back-up my essential data before doing anything to the partition. There are also commercial utilities to change the partition size without destroying the content of the partition.

My preference is to do a clean re-install of MS Windows on a single, dedicated partition. I leave some space on the hard unpartitioned so I can use later for Linux. My fair division of hard drive space between MS Windows and Linux is 50/50. Linux programs tend to be smaller but they include a standard component that MS Windows offers only with thousands of dollars of add-ons: e.g., servers (not just clients) for telnet, ftp, http, and mail, several databases, programming languages...

# 1.11 How do I install the installation?

Insert the installation boot disk into your drive, the RedHat CD to the CDROM, and reboot. If you booted from the CD, insert the RedHat CD into your CDROM drive and reboot.

You may also start the installation from DOS (real DOS mode under MS Windows), by running EZSTART._BAT on your RedHat CD from Cheabyetes.

# 1.12 Is the Linux installation difficult?

It was not for me. It seems that for most newbies, its fairly straightforward and painless. Depending on your hardware and installation conditions, it typically takes 0.5 h to 2.0 hours. [Except longer or possible problems for low systems with restricted memory--it took me whole to install RH on my 486-33 MHz with 8 MB memory, the system pausing for 5 minutes at a time appearing to do nothing, yet installed ok.] However, some newbies reported that the installation was a "total nightmare" to their hard problems?). If you encounter problems, my advice would be to install a plain-vanilla system, without struggling with the high resolution on your fancy video card or some bleeding-edge hardware which you might have. Anything can be added/configured later, after you get more understanding of how things work on your system. A re-install is always an option for a newbie (it seems Linux guru think it is a shame to ever re-install). It seems that many newbies have problems because they specify too high screen resolutions (which may not be supported or supported only with some extra tune-up). Again, it may not be to break your whole installation for support of a single device--the support can be added/tuned up later.