# Question 6

Which of the following drivers is definitely not associated with a CD-ROM drive?

+   - a. /dev/sdd
+   - b. /dev/sbpcd
+   - c. /dev/hdb
+   - d. /dev/hda3

Answer d is correct. It is actually the third primary partition on the first regular hard disk. CD-ROMs are generally not split into separate volumes. The /dev/sdd driver is for the fourth SCSI drive. Because it does not list a volume number, it may be a CD-ROM drive. Therefore, answer a is incorrect. The /dev/sbpcd driver is the CD-ROM attachment to an older Sound Blaster card; therefore, answer b is incorrect. Because the /dev/hdb drive is a common device for a CD-ROM on a computer that also has a regular hard disk, answer c is incorrect.

# Question 7

Which of the following file systems is not "real"?

+   - a. /bin
+   - b. /opt
+   - c. /root
+   - d. /proc

Answer d is correct. The /proc file system does not list any actual files. Instead, it lists currently running programs and kernel routines. The /bin file system includes many standard Linux utilities, so answer a is incorrect. The /opt file system is where many applications are installed, so answer b is incorrect. Because the /root file system is the home directory for the root user, answer c is incorrect.