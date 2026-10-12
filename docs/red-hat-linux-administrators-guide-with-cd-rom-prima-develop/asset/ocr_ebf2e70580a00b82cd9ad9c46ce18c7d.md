+   signals to control timing sensitive applications, and can support alarms. You will have to provide additional settings elsewhere in the software to ensure that the hardware time stays correct.
+   
+   - **Line 41** displays the RAM disk drive, which allocates a portion of your physical RAM for saving files and for accessing often used files. This is not always the most effective use of RAM since the Linux buffer cache does the same automatically. Most commonly RAM drives are used during the initial Linux install process.
+   
+   - Next, Linux determines what types of physical hard drives, CD-ROMs, and floppy drives are installed on the computer. This is covered on lines 42–53. There is one Maxtor 20 gigabyte IDE drive, one ATAPI CD-ROM, and no floppy drives.
+   
+   - On lines 54–64, the startup process initializes the RAID code and optimizes the fastest method of computing checksums on the RAID. Locating and mounting RAID devices comes later.
+   
+   - **Lines 65–67** list the partition check results. These are the partitions as you set them up during the initial install.
+   
+   - **Lines 68–70** show the kernel detecting any additional RAID arrays and beginning the autorun sequence, which attempts to find all drives that belong to each RAID set.
+   
+   - Next, on line 71, the root file system is mounted using the ext2 file format.
+   
+   - **Lines 72–79** define the SCSI controller card and verify that certain requirements are met in order for the card to function properly under Linux. The “0:2:0” notation means “channel # : SCSI ID # : LUN”.
+   
+   - Once the SCSI card has been properly detected, any peripheral devices are then displayed. The two devices displayed are both SCSI tape backup devices. Linux displays their makeup under lines 80–85. The first has a SCSI ID number of 2 and is an internal HP auto tape loader, while the second is an external single-tape backup device. They are assigned the same driver and identity.

# NOTE

Rather than poring over the dmesg file once the operating system has been loaded, you can reaffirm the identity of your SCSI devices by typing *cat /proc/scsi*. This will display all devices attached to your SCSI card.