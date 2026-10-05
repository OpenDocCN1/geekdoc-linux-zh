# INSTALLATION

Then you can select, using the cursor keys ← and →, at which point the partition should be divided into two smaller partitions. (The partitioning point should only be specified within the unused area of the partition. It is good practice to leave a couple of Mbytes free on the partition to be divided, otherwise it will hardly be possible to carry out reasonable work on it later on.) After several safety questions, the partition is permanently divided. (You may abort the program at any time by pressing Ctrl+C if you don't feel completely about what you are doing!)

Now, when you reboot your computer, DOS and Windows should work as before. However, the amount of free disk space should be considerably lower. But you have acquired new empty partition. If you want to use this partition under DOS/Windows, you must format it with the FORMAT command. More probably, though you want to use this partition under Linux: FDISK delete the partition. (During the installation of Linux, you will create a new Linux partition in this area of the hard disk, which is now completely free.) Details of how to use FDISK follow in the next subsection.

FIPS also comes with extensive (English) online documentation: fips.doc describes the use of the program, errors.txt contains list of possible error messages and a short description, and techinfo.txt gives technical background information (for those who are interested). Current information on FIPS can be found on the Internet:

http://www.igd.fhg.de/~Taschaefe/fips/

# Repartitioning your hard disk with FDISK

It has already been mentioned that deleting a partition with the FDISK program causes a complete loss of all data stored in that partition. Therefore, a backup of all your data is compulsory!

This is, however, not the only problem: you must also ensure that the execution of FDISK has the necessary diskettes to reinstall DOS or Windows and then restore the deleted data. (After deleting the partition with FDISK, neither DOS nor Windows is available anymore!) Frequently, the problem consists in the fact that you have been supplied by your dealer with a preconfigured system. Installation of Windows 9x or Windows NT on a 'naked' computer (without any installed operating system) is not as complicated as the installation of Linux – that it is much worse done.

Since this is a book about Linux (and not Windows 9x or NT technical reference manual), I must unfortunately leave you to your destiny with your Windows reinstallation. Although I am not a shareholder in any hard disk manufacturing company, I would at least consider buying a second hard disk instead of reinstalling Windows. Not only do you gain more space, but you also have more flexibility and greater safety. Another variation is to ask your dealer for a reinstallation in a reduced partition.

![](bbox=[0.195, 0.403, 0.235, 0.473])