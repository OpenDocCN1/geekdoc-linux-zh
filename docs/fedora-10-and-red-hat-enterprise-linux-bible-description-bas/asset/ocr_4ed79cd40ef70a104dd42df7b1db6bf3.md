# Part II: Using Fedora and RHEL

```
http://download.fedora.redhat.com/pub/fedora/linux/releases/7/Fedora/i386/os
```

NOTE: Here's how to use your Fedora DVD as a Xen guest repository. Install the nfs-utils package.
Insert the DVD. As it is mounted as /media/disk, add the line:

/media/disk * ( ro)
to the /etc/exports file. Start nfs (/etc/init.d/nfs start). When you are prompted for a software repository, enter this address: nfs:localhost:/media/disk. If localhost doesn't work, try your computer's IP address.

+   **8. Storage location** — Choose to use a file on an existing file system or the device name of a partition to the installed system. For example, you could name the disk image /home/chris/xenimage as the file to use. I created a new partition as I was doing this process. Just make sure the location you use has enough disk space to hold the operating system you are to install. You are asked to allocate memory.

+   **9. Host network** — Choose how you would like your virtual system to connect to the host network. In most cases, select Virtual network. However, you can also select a physical device (such as an Ethernet bridge or MAC address).

+   **10. Allocate Memory** — Type a number representing the number of megabytes of RAM you dedicate to this virtual machine and the amount you want to start with and click Forward. At least 256 megabytes of RAM are recommended. If you have more available, should use more since it will improve performance. You can also select to use multiple CPUs (1 is the default).

+   **11. Finish** — When all the information has been entered, a summary of the information you entered appears shown in Figure 5-6. Finish The new virtual machine will appear on the Virtual Machine manager. Select it and click Open.

+   **12. Start installation** — A virtual console should appear, ready to install your guest Fedora 7 installation.

+   **13. Install Guest** — Because you are installing a Fedora 7 on a Fedora 10 system, you can basically follow the installation instructions in Chapter 2 of this book. By for partitioning, you can instruct the installer to use the entire partition or you can create multiple partitions.

After Fedora is installed, you can open that virtual machine as you need it from the Virtual Machine Manager window. If you selected Ethernet bridging, and there is a DHCP server on your network, your virtual machine can be assigned its own IP address. You can use tools in Fedora to access the Internet and update and get new software as needed.

To manage your virtual machines from the command line you can use the xm command. To see which virtual machines are currently available, type the following: