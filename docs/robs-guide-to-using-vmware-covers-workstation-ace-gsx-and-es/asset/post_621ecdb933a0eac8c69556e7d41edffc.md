
consideration if you will be running CPU intensive applications inside your guest operating systems. Running a file and print server for 50 users relies more heavily on disk and network access instead of CPU usage, compared to a server running a high end Java2 Enterprise Edition application that is continuously accessed by several hundred users.

Choosing the number of CPUs for the virtual machines that you plan to run cannot be done without looking into other factors, such as hard disk and network activity which will impact your server's performance. As an example, let's assume that you have a four processor machine and you are planning on running the suggested sixteen virtual machines. This may sound good on the processor side, but if that server has only one hard disk that all virtual machines need to read from and write to, you will end up with poor performance, even with non-disk intensive applications.

## Memory

The second component of your server that will heavily influence the performance of your virtual machines is the available memory. A general rule with most servers and operating systems is: the more the better. But there are a few things to keep in mind before ordering all your servers with 64 GB by default.

First of all, you need to determine how much memory you really need for your virtual machines and how much memory you need for future installations. The great advantage of VMware's current generation of products is that it does not pre-allocate the memory that you assign to a virtual machine. In other words, if you start four machines with 512 MB each, your GSX Server software does not consume 2 GB of memory from the start. If those guest operating systems are only using 256 MB each, the total memory usage will be around 1 GB or even less.

When you encounter such a situation, you can optimize the memory settings of your GSX Server and virtual machines. Therefore, when calculating the amount of RAM that you really need for your server, you do not have to add up the amount of RAM that you would typically buy for your independent physical servers. Of course, you also benefit from using VMware technology with the capability of removing and adding memory to virtual machines very easily, especially compared to swapping physical memory modules.

> Note: It is important to remember to reserve enough memory for your host operating system. When your host OS starts using virtual memory (for swapping, paging, etc.), the performance of your virtual machines will degrade noticeably.

For configurations of up to 4 GB, there are not too many special configurations that you have to consider. As long as you remember that besides the amount of RAM required to run a given number of virtual machines, you also need to have sufficient processing power and hard disk availability.

When you plan to exceed 4 GB with the VMware GSX Server, you need to look into some special configurations. Whether more than 4 GB can be used will depend on your hardware platform and your operating system. First, let's take a look at the 32 bit architecture. The memory limit for an Intel 32 bit systems is 4 GB. With the support for Physical Addressing Extension (PAE), this memory limit can be extended. The amount of memory you can use depends on your operating system. With Windows 2000 Advanced Server, the limit can be extended to 8 GB and for Windows 2000 Datacenter Server the limit is 32 GB. For Windows Server 2003, the limit of the Standard Edition is always 4 GB because it does not support PAE. With Windows Server 2003 Enterprise Edition the limit is automatically extended to 64 GB.

To enable PAE on a Windows host, you need to edit the boot.ini file and add the /PAE switch to the end of the line, where you load the operating system. The following is an example of a Boot.ini file, where the PAE switch has been added:

```
[boot loader]
timeout=30
default=multi(0)disk(0)rdisk(0)partition(2)\WINDOWS
[operating systems]
multi(0)disk(0)rdisk(0)partition(2)\WINDOWS="Windows Server 2003, Enterprise" /fastdetect /PAE
```

Whether Linux supports PAE depends on your distribution. You will have to check with your vendor if you want to use more than 4 GB of RAM on your Linux host. However, most of the recent professional distributions from SuSE and RedHat support PAE.

## 64 bit platform

On the 64 bit platform with Windows Server 2003 for 64 bit Extended Systems, the operating system can handle 64 GB by default. The 32 Bit applications, such as VMware GSX Server, run in a subsystem that accommodates loading, execution, and management of 32-bit applications. This subsystem is called WOW64, or Windows-32-on-Windows-64. This subsystem only assigns 4 GB to a 32 bit application. There is one slight advantage over the typical 4 GB, which you get on a normal non-PAE enabled system. In this case, the memory is also used by the operating system and other applications. Whereas on the 64 bit platform, the application is assigned a total of 4 GB for dedicated use (as long as the server has more than 4 GB total, so the OS itself and other applications are loaded in the remaining available memory).

Therefore, the bottom line is that you will get some benefits from buying a 64 bit platform to run VMware GSX Server but you might want to spend your money on an additional optimized 32 bit server to balance the load of your virtual machines.

Note: All this information about the 64 bit platform does not cover running 64 bit guest operating systems. If you need to do that, you need to buy a 64 bit platform first and it is important to know that VMware GSX Server runs on that hardware.

Note: Support for the 64 bit platform is something that most likely will become available with version 3 of VMware ESX Server. There is no information available at the time of writing this book to suggest that a 64 bit version of VMware GSX Server or VMware Workstation will become available soon.

## 3.2 Upgrading GSX Server Software

For both Windows and Linux, it is important to take the following actions if you are going to install a newer version of VMware GSX Server. This is especially important if you are planning to install from an older generation of GSX Server. As an example, if you are running GSX Server version 2.x and are now upgrading to version 3.2:

- 4. Make sure that all virtual machines are in the Power Off state. If your machines are suspended, resume them first, shut down the guest operating system and then power them off. After installing the new GSX Server software, you will need to upgrade the virtual hardware. See the GSX Server Administration Guide if this applies to you. Also check out the information about VMware generations on page 98.
- 5. Save all undoable disk mode information into the virtual disks. When you have disks that are in the legacy undoable mode, make sure that you save all the changes into virtual disks or discard the changes before powering off.

Also, make sure that you create a backup of your virtual machines and your GSX Server Host machine. And last but not least, test the newer version of VMware GSX Server before you install it into your production environment.

Before you can install a newer version of VMware GSX Server on Windows, you must uninstall your current version. For Linux, it depends on the previous installation method. If you have used the tar installer, you do not have to uninstall the previous version. You only need to ensure that no old extracted files from a tar installation exist in the directory where you extract your download. When you use the RPM installer, you must first uninstall the current version before you can install a new one. To find out whether you have installed with the RPM package, use the following command to query the RPM database:

```
rpm -qa | grep VMware
```

If no entry from the database is shown, then you can assume that the installation was done with the installer from the tar archive. If you need to uninstall the application, which was installed with the RPM package, use the following command:

```
rpm -e VMware-gsx
```

The RPM database listing that you performed with the query command shows all the installed software. The keyword VMware-gsx is used to uninstall the GSX Server, but the VMware console could also be shown in this listing.
