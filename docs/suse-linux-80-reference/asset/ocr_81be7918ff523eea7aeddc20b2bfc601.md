# Starting Your System from the CD-ROM

Insert the first SuSE Linux CD or the DVD into the drive. Then, restart the computer to load SuSE Linux, install from the medium located in the drive, and set up your machine.

# The Opening Screen

As the boot screen appears, SuSE Linux is preparing the installation. Follow its progress in the segmented bar on the left.

If your machine does not boot from the CD-ROM, change the settings in the computer’s BIOS. At initial start-up, a diagnosis of the computer’s hardware is conducted and, among other things, the random access memory is tested. Recognize this by the system memory count. At the bottom of the screen, the key that calls up the BIOS setup is listed — usually (Del) or (F1). Press the key specified to access the BIOS setup.

If your machine is equipped with an AWARD BIOS, the relevant entry is labeled BIOS FEATURES SETUP. Other manufacturers use similar entries, such as ADVANCED CMOS SETUP. Select the corresponding entry and confirm with (↵). Relevant for your purposes is the subitem normally listed as ‘Boot Sequence’.

The default setting for this is usually C, A or A, C. In the first example, when booting, the machine searches for boot information on the C drive then on the A drive. Select ‘Boot Sequence’ then press (PageUp) and (PageDown) until the A, CDROM, C sequence is shown.

Next, exit these settings by pressing (Esc). To save the changes, select ‘SAVE & EXIT SETUP’ or press (F10). At this point, you will be asked if you want to exit the BIOS setup and save these new settings.

If you have a SCSI CD-ROM drive, access the controller’s BIOS — in the case of an Adaptec host adapter, with (Ctrl) + (A). Select ‘Disk Utilities’. The system checks the hardware installed and displays the corresponding information.

Make note of the SCSI ID for your CD-ROM. Next, exit the menu with (Esc). Open ‘Configure Adapter Settings’. You will find ‘Boot Device Options’ under ‘Additional Options’. Select this menu and press (↵). Now enter the CD-ROM drive ID and press (↵). Return to the start screen in the SCSI BIOS by pressing (Esc) twice, which can be exited by confirming with ‘Yes’ to reboot the machine.

A few seconds later, SuSE Linux starts loading a minimal Linux system that takes over the rest of the installation procedure. A number of messages and copyright notices then appear on the screen. At the end of the loading process, the YaST2 program will start, and a few seconds later, the graphical interface of YaST2, the SuSE Linux installation program, is displayed.