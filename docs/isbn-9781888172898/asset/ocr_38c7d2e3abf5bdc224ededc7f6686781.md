![](bbox=[0.1, 0.1, 0.9, 0.42])

Figure 2.17: Installing LILO

Here are the "rules" of where /boot must live if you want to install LILO on a hard drive:

+   1. If you have 2 IDE (or EIDE) drives, /boot must live on one of them. This also includes any IDE CD-ROM drives on your primary controller. If you have one IDE hard drive, and one IDE CD-ROM on the primary controller, /boot must live on the hard drive.
+   2. If you have one IDE (or EIDE) drive and one or more SCSI drives, /boot must live either on the IDE drive or the SCSI drive that is at ID 0. No other SCSI IDs will work.
+   3. If you have SCSI only, /boot must live on a drive at ID 0 or ID 1. No other SCSI IDs will work.
+   4. In any case, /boot must live below cylinder 1023. For IDE (or EIDE) drives, this generally means below the 512 MB mark; for SCSI drives, it's generally below the 1 GB mark.

# Adding Options to the LILO Boot Command Line

Finally, the installation program will ask if you wish to add default options to the LILO boot command. Any options you enter will be passed to the