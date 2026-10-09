# LINUX INSTALLATION REQUIREMENTS



Table 2-4
Common peripheral port settings.

| Device | I/O Address | IRQ |
| :--- | :--- | :--- |
| Serial Port 1 | 3F8 | 4 |
| Serial Port 2 | 2F8 | 3 |
| Serial Port 3 | 3E8 | 4 |
| Serial Port 4 | 2E8 | 3 |
| Parallel Port 1 | 378 | 7 |
| Parallel Port 2 | 278 | 5 |
| Sound Port | 220 | 5 |

include the I/O address and the Interrupt Request (IRQ). The I/O address is the memory address the system uses to communicate with the device. An Interrupt Request is a signal the system uses to indicate when time will be spent by the system accessing the device. Some of these values are listed in Table 2-4.

Many settings for ports seem to conflict with each other, but that is generally not a concern. For example, a system may have two serial devices, one using IRQ 3 and the other using IRQ 4, but using more than two serial ports is generally not necessary. The additional settings are typically used when a conflict arises.

# SOFTWARE AND SERVICES

Objective 1.5

The software and services that are available on a Linux system reflect the function of the installation. A personal desktop would usually need the GUI and personal productivity software, but not server services, such as Dynamic Host Configuration Protocol (DHCP) or Domain Name System (DNS). Software can always be added if enough resources are available, but you should plan your software and services implementation before installation to ensure that the resources available are sufficient.

Table 2-5 is taken from a Red Hat Linux distribution. Not all distributions have the same software, but it is a good example of the software and services you can expect to find.

You may intend to install commercial software on your system. You should contact the software vendor and make sure the Linux distribution you choose is supported. There may be a version of the software you can run “out-of-the-box,” or it may need to be compiled for your specific installation.

Some commercial software packages require a lot of disk space to install, and even more to run. The amount of disk space needed can be calculated by the software vendor.

# ALLOCATING STORAGE SPACE

Nearly every computer system today uses disk partitions. Partitions are a standard in the computer industry. However, with so many preconfigured computer systems, many users don’t understand how disk partitions work or even what they are.

Hard disk drives are relatively simple devices, or at least they’ve been around so long that the approach to using them is very standard. Their purpose is to store data and reliably retrieve it.

A hard disk is designed to be “formatted” for the specific operating system that will be controlling it. By formatting a drive you are creating a file system on the drive. A file system uses a small percentage of the drive space to accomplish its task of organizing the storage structure of the data. It divides the remainder of the drive into small segments called blocks. There are several file systems that are not necessarily standard between different operating systems. For example, a Linux ext3 file system is not readable by a Windows NT system, and the Windows NT NTFS file system is not fully available to a Linux system. (NTFS file systems can be read by Linux, but write support is not yet available in all