2. After these diskette image files are downloaded, use typical tools to write to floppy diskette. For Windows, this usually means rawwrite. The rawwrite program for Windows can be found here:
http://www.chrysocome.net/rawwrite

After you have written the diskette image to a floppy disk, remove the disk so that you can use it to install DSL on the target machine. (Later, when instructed to boot from either of these two floppies, be sure that you have changed your system’s BIOS setting so that the floppy is the first boot device.)

# DSL Installed on Windows 9x or DOS Partition

Let’s say you have a Windows 9x or DOS system with modem or Internet access and you want to try DSL. You do not want to disturb your Windows installation. You especially do not want to have to repartition your hard drive. To install DSL without affecting your current system, follow these steps:

NOTE
Internet access is required for this section. Methods for system without Internet access will be discussed in the next section of this chapter.

+   1. Boot the machine on which you want to install DSL into Windows or DOS.

+   2. Download the embedded version of DSL to C:\. We are not going to attempt to run virtualization as discussed in Chapter 7. The embedded version is provided as a Zip file and therefore is very easy access for DOS and Windows system to unzip.
+   
+   The embedded version, which I will call the Zip file version of DSL, can be found here:
+   ftp://ibiblio.org/pub/Linux/distributions/damnsmalllinux/current/dsl-embedded.zip

+   3. If you have an unzip program on your Windows system, unzip this Zip file into a working directory—for example, c:\work.
+   If you do not have unzip, you can reboot your computer using the DSL Utilities boot floppy and you will find unzip and other utility programs that we will be using.