
2. After these diskette image files are downloaded, use typical tools to write to floppy diskette. For Windows, this usually means rawwrite. The rawwrite program for Windows can be found here:
http://www.chrysocome.net/rawwrite

After you have written the diskette image to a floppy disk, remove the disk so that you can use it to install DSL on the target machine. (Later, when instructed to boot from either of these two floppies, be sure that you have changed your system’s BIOS setting so that the floppy is the first boot device.)

## DSL Installed on Windows 9x or DOS Partition

Let’s say you have a Windows 9x or DOS system with modem or Internet access and you want to try DSL. You do not want to disturb your Windows installation. You especially do not want to have to repartition your hard drive. To install DSL without affecting your current system, follow these steps:

NOTE
Internet access is required for this section. Methods for system without Internet access will be discussed in the next section of this chapter.

- 1. Boot the machine on which you want to install DSL into Windows or DOS.
- 2. Download the embedded version of DSL to C:\. We are not going to attempt to run virtualization as discussed in Chapter 7. The embedded version is provided as a Zip file and therefore is very easy access for DOS and Windows system to unzip.
- The embedded version, which I will call the Zip file version of DSL, can be found here:
ftp://ibiblio.org/pub/Linux/distributions/damnsmalllinux/current/dsl-embedded.zip
- 3. If you have an unzip program on your Windows system, unzip this Zip file into a working directory—for example, c:\work.
If you do not have unzip, you can reboot your computer using the DSL Utilities boot floppy and you will find unzip and other utility programs that we will be using.

I will now focus on using the DSL FreeDOS Utilities diskette. Doing so allows a common base on which to proceed. If you already have unzip and are familiar, I am sure it will still be easy to follow along.

### NOTE

If you have Windows XP, the FreeDOS boot floppy utilities will not work. With XP, you already have unzip; therefore, it is not needed.

Boot from the utilities diskette and then perform the following:
A:\> C:
C:\> unzip dsl-33-1.zip KNOPPIX/KNOPPIX

### NOTE

The DSL Zip file name is munged because of the DOS 8.3 filename limit. With FreeDOS, you can type just a few characters and press the Tab key and the munged filename will be auto completed. If using Windows, you will probably be able to see and use the full Zip filename.

- 4. Replace the DSL Utilities diskette with the DSL boot floppy and reboot your system using the DSL boot floppy.
- 5. At the DSL boot prompt, type the following:
boot: dsl 2 legacy frugal
While booting from the DSL boot floppy, if errors appear or the system hangs, you likely need to use additional boot options. DSL boot options are discussed in Chapter 2.
- 6. When you see the system prompt #, enter the following:
# mkdoss swapfile
Reboot again and you have arrived at a Poorman's installation of DSL.
Congratulations! You are now running a DSL Poorman's installation within a Windows or DOS formatted partition.

## DSL Installed on an Existing Linux Partition

The Poorman's method is also available within an existing traditional Linux installation. You may have another Linux distribution and want to try the Poorman's installation method. The steps are really the same as earlier:

- 1. Download the embedded version of DSL (the Zip file).
- 2. Unzip to extract only the KNOPPIX/KNOPPIX file as a level one directory on a Linux partition.
- 3. Boot your system from the DSL boot floppy.

During boot, your partitions are scanned for the KNOPPIX/KNOPPIX file and begin to boot DSL. Again, you may need to specify additional boot parameters just as you would do by booting from the DSL CD-ROM.

## FRUGAL DSL INSTALL ON WINDOWS 9x OR DOS

Recall from the earlier definition of Frugal: A Frugal install is a Poorman's installation sans floppy diskette and without having to type additional boot options. The procedures discussed next apply to DOS, Windows 95, and Windows 98. Only systems that can boot to DOS native mode are supported. Windows ME can be patched to boot DOS native, but that is beyond the scope of this discussion. If you have Windows XP, you may want to use virtualization as discussed in Chapter 7.

Before you try these procedures, you should successfully perform the Poorman's installation in the preceding section. In fact, if you have found that you are in need of additional boot parameters, you should have them written down. The goal here is to have no floppy and not have to type additional boot parameters upon each boot.

### Booting DSL from Native DOS Mode Using LinLd

The linld boot loader is a tiny DOS COM file. With linld, you can type all the boot information on the DOS command line similar to the DSL boot prompt, or you can use a simple DOS text file to store the boot options.

For more information on LinLd, see the announcement at

http://www.lwn.net/Articles/102210/

Let's continue on from our Poorman's method. You need to have Poorman's setup (in other words, you should have the C:\KNOPPIX\KNOPPIX file in place and the Zip file still resident on C:\ as well). Then, boot from the DSL FreeDOS Utilities diskette and perform the following:

```
A:\> C:
C:\> unzip dsl-33-1.zip linux24
C:\> unzip dsl-33-1.zip minirt24.gz
```
