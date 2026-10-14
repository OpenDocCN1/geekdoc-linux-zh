+   - Are installing from the Network.
+   - Are installing from a SCSI CD-ROM.

If your system is fairly standard, it is unlikely that you’ll need the second disk, but build it anyway just in case you do. To build the floppies, follow these steps:

+   1. Boot your computer into DOS or Windows.
+   2. Insert the Linux CD-ROM into your computer. (I am assuming that your CD-ROM is located in drive D. If it is located elsewhere, substitute the correct drive letter).
+   3. Insert a 3 1/2" 1.44MB diskette into the floppy drive.
+   4. At a DOS prompt, enter `d:\col\launch\floppy\rawwrite3`.
+   5. Enter the full pathname to the disk image file: `d:\col\launch\floppy\install.144`.
+   6. Provide the drive letter for the floppy diskette (typically A) and press Enter.

To build the modules diskette, repeat steps 3–6 but provide the name of the modules image instead: `d:\col\launch\floppy\modules.144`.

Note that `rawrite3` sometimes has trouble with Windows NT 4.0 systems and with some computer system BIOS chips. If `rawrite3` fails to produce working disks on your computer, you might need to borrow a friend’s computer for a few moments to make working install and modules disks.

# Starting the Install

If your computer doesn’t support booting from a CD-ROM, insert the install diskette and start your computer. After a few seconds you’ll see the Linux boot prompt. Hit return to start the installation process.

If your computer supports booting from a CD, put your CD into the CD-ROM, verify that your BIOS is set to boot from the CD (see your computer’s manual), and start your computer. Booting from the CD is the fastest way to install Linux on your computer.

Either way, after a few seconds you’ll see the installation screen and a `boot :` prompt. Hit Enter to expedite the process; otherwise, you’ll have to wait about 20 seconds before the installation boot begins. After the boot process begins, you’ll see text scrolling up your display for up to a minute; it is safe to ignore these progress reports.

# Language Selection

After the boot process is complete, you’ll be prompted for the language you want to use during the installation. Select whatever language is appropriate for you. Use the arrow keys to change the selection. When the option you want is highlighted, press Enter. Note that while installing, the button with the white text is the selected option. This is not always obvious.