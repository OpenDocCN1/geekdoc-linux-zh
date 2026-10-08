+   2. Right-click the $3 \frac{1}{2}$ Floppy $(A:)$ icon and choose the Format option.
The Format $A: \backslash$ window appears.
3. Click the Make a Bootable Disk option and then the Start button.
A confirmation window — labeled Format $A: \backslash$ again — opens.
4. Click the OK button and your floppy is formatted.

The Publisher’s Edition Red Hat Linux DVD-ROM, bundled with this book, unfortunately doesn’t include the FIPS utility. However, you can download FIPS to the floppy disk you just created:

+   1. Open your browser and go to www.redhat.com/download/\mirrors.html.
2. Select any Red Hat mirror.
*Mirrors* are just that — mirror images of downloadable software. Many organizations help out the open source movement by providing their resources, such as Web pages that allow you to download software, to spread the burden of distributing software. Red Hat Linux, a popular download site, greatly benefits from mirrors.
3. When your browser displays the mirror you selected, go to the sub-directory redhat/8.1/en/os/i386/dosutils/fips20 if you’re using Windows 98 or Windows Me or the newer version of Windows 95 (or Windows NT, Windows 2000, or Windows XP systems that happen to use FAT file systems).
Alternatively, go to redhat/10/en/os/i386/dosutils/fips15c if you’re using an older version of Windows 95.
For instance, go to the University of Oregon Red Hat mirror, at ftp:// limestone.uoregon.edu/redhat/8.0/en/os/i386/dosutils.
4. Download fips.exe, restorrb.exe, errors.txt, and, optionally, readme.1st and fips.faq to your floppy disk.
5. Boot your computer from the floppy disk.
The computer restarts in MS-DOS mode.
6. Type cd a:\ at the DOS prompt and press Enter.
7. Type fips at the prompt and press Enter.
Some messages appear and flash by, but you can ignore them all except the last one, which asks you to press any key.
8. When you see the Press any key message, do so.
You see all existing partitions on the hard drive.