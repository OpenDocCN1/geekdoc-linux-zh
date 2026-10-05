# REPARTITIONING YOUR HARD DISK UNDER DOS/WINDOWS 27

it is necessary to defragment the disk beforehand. During this process, the sectors occupied by one file are shifted so that they are contiguous (whereas when the disk is fragmented the sectors of a file may be distributed over the disk). The first part of the partition is the fully occupied one, the last part is free. Disk access is somewhat faster than in the fragmented state. (Fragmentation occurs through normal use of the hard disk, that is, through creation and deletion of files of different sizes.)

Before you start defragmenting, you should check the partition for defects CHDSK under DOS, SCANDISK under Windows 9x and delete any detected sectors that are no longer assigned to a file.

Under DOS 6.0, defragmentation can be carried out with the DEFR program. Under Windows 5, you click the mouse button on the disk symbol in the Explorer, select the context menu entry PROPERTIES, dialog tab EXTRAS, and in the pop-up dialog, select the button OPTIMIZE NOW. You can sit back and watch this program working if you click the DETAILS button.

The problem with the use of defragmentation programs is that they consider some system files as not being relocatable. If you are unlucky, and a non-relocatable file lies towards the end of the partition, FIPS cannot reduce the partition to its full extent. The FIPS documentation gives a couple of hints regarding the origin of such files, but these are valid only for DOS or Windows 3.1.

Unfortunately, it is not known which files are considered as non-relocatable under Windows 9x. (On my computer, one such file made the application of FIPS quite useless. A non-relocatable file was found in the last 5% of a 50% free 300 Mbyte partition. It was impossible to find out which file this was. I cannot tell whether defragmentation programs (from other suppliers yield better results).

If the defragmentation results are not satisfactory, you can try searching the hard disk for non-relocatable files and manually resetting their system and hidden attributes. The DOS command ATTRIB /S.* writes a list of the attributes of all the files on your hard disk into a text file.

You can now easily read this file with any editor and subsequently to change the system and hidden attributes of individual files, either with ATTRIB or in the Explorer (secondary mouse button, context menu PROPERTIES). Caution is highly recommended - refrain from modifications in the root directory itself and be careful with the swap file! After this, execute the defragmentation program once more and hope for the best.

Next, you must create a DOS boot diskette (FORMAT A:/S) and copy the programs FIPS and RESTORRB together with the text file error.txt onto it. With this diskette, you reboot your computer and execute FIPS. (Do not start FIPS directly from a running system - by doing so, you run a considerable risk).

The usage of FIPS is pretty straightforward: the program analyzes the hard disk and displays the result of this analysis. The current partition information (root and boot sectors) can be copied onto the diskette, so that in case of problems the partition can be restored with RESTORRB.

![](bbox=[0.135, 0.535, 0.155, 0.585])