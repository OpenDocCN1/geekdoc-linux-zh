# **NOTE**

Using fdisk you can define what type of OS you would like to install on a particular partition. Fdisk allows you to choose between 78 different file formats, anywhere from a Windows 95 file allocation table (FAT) to Novell Netware or even AIX. Fdisk allows you to change a partition's ID to another operating system by typing t at the fdisk command line. You may list all available file types by typing l on the same line. Disk Druid presents you initially with only a five or six different file formats.
After installation you can still change the partition format. Type /sbin/fdisk and the partition name. A typical command would be /sbin/fdisk /dev/hda.

Once you have either set a new partition or changed a partition's ID using fdisk, you will need to write the information to the partition table and then exit. You should use fdisk only during the initial installation or when defining the remaining free space on the drive for another operating system.

As Linux continues to gain importance and notoriety, more and more users are demanding easier- to-use partitioning tools. Red Hat meets many of these demands by further developing Disk Druid and by assisting in setting up separate partitions for both Linux and other operating systems such as Microsoft, DOS, Be, and OS/2. Each can be allotted its own partition. Red Hat also allows you to define which operating system is the default.

# ## Determining the Function of Your Linux Box

Before partitioning hard drives for use on a Linux machine, you, first must answer several questions:

+   - What is the basic function of this machine?
+   - What partition will require the most space based on the machine's primary function?
+   - Will the software need to be reinstalled or upgraded at some later date?
+   - Will there be a need to expand the existing hardware at some later date?

The first two questions are probably the most important and are linked in purpose. If this Linux box is to function as a web server, it will need more space either on the /home or /usr/local directory. If, however, it is to be a news server