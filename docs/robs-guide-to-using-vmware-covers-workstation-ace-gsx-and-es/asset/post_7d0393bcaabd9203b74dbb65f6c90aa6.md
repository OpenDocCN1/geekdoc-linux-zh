
9. When the modules are loaded, the configuration script will prompt you with questions regarding networking. Answer these questions according to your needs.

- Do you want networking for your virtual machines?
  (default: yes)

- Do you want to be able to use NAT networking in your virtual machines?
  (default: yes)

If you select to install NAT:
Do you want this program to probe for an unused private subnet?
(default: yes)
You will also be prompted with a question to configure additional NAT networks. The default answer is: no.

- Do you want to be able to use host-only networking in your virtual machines?
  (default: yes)

If you select to install host-only networking:
Do you want this program to probe for an unused private subnet?
(default: yes)
You will also be prompted with a question to configure additional host-only networks. The default answer is: no.

10. After the configuration script has finished successfully, you can start the VMware Workstation. There is no need to do that as a root user, so execute the exit command to return to your previous user environment. Start the application with the following command from the command line:

```
/usr/sbin/vmware &
```

Tip: The ampersand sign (&) has been added to run the application in the background when the GUI application starts. This is to prevent your running shell to be stuck on this command. You probably have enough windows open already and we do not want too many windows open; do we?

11. The final step to finish your installation is to add your VMware Workstation for Linux license. In the VMware GUI application, select Help → Enter Serial Number to add the license.

After the installation is complete, you can create your first virtual machine. Before you do so, make sure that you understand what types of disks and networking you can choose. Continue with paragraph 2.6 to read more about disk types and networking options.

## 2.6 Disk Types for your Virtual Machines

Before you can create your first virtual machine, you will have to understand your options for using hard disks and networking first.

VMware Workstation virtual machines will run with virtual disks which will not in any way affect your host computer’s hard disk. You can create partitions in your virtual machine, format your disks, and defragment them. None of these actions will directly interfere with your physical hard disk. Everything happens in one or more virtual disk files that form your virtual hard disk.

The only relationship with your host hard disk is that your host operating system is transferring data to and from your physical disk. Your guest operating system is accessing the same physical disk by using the virtual disk files. You can imagine that disk intensive operations will slow down your PC dramatically if you are running multiple PCs simultaneously on a single disk channel.

You have three hard disk options when creating new virtual machines.

- A virtual disk that will **grow dynamically** to the maximum virtual hard disk size.

This is the default option, as well as the option that is used when doing a typical creation of a virtual machine. **I recommend using this disk type if you are just getting started with VMware Workstation.** A .vmdk disk file that is only a few kilobytes in size will be created. The .vmdk file grows dynamically; this is only the case if you start putting data on the hard disk from the guest operating system, during installation and afterwards (when working with the machine).

The advantage is that your virtual machine will only take as much space as is really needed by your guest operating system and its applications and data. You can create a 100 GB disk that will start small and grow to 1 or 2 GB after installation without ever using the entire 100 GB on your host PC.

The disadvantage of this disk type is that with the file becoming larger over time, it will become very much defragmented on your host PC’s hard disk and will make it slower. Growing the disk also has a negative impact on performance.

These dynamically growing disks are not automatically shrunk. You will have to go through a manual process described elsewhere in this book to decrease the size of your virtual disk file.

- A virtual disk that has a **fixed size** equal to the maximum virtual hard disk size.

When creating a virtual disk from the New Virtual Machine Wizard, you can enable a check box for your virtual machine to **Allocate disk space now**. This option allows the VMware Workstation to create a virtual disk file which has the same size that you specify for the virtual hard disk on the host PC. Creating a 100 GB virtual hard disk would take up 100 GB of hard disk space on your host PC’s hard disk.

The advantage of this disk type is that even though it may take longer to create the disk, running the virtual machine is still faster because the disk will not be so defragmented on your host PC’s hard disk. This is only true if you make sure that there is enough space to sequentially create the entire file. Use the Windows Defragment utility to analyze this before and after you create the file.

You will need to use this type of disk if you want to use a clustering solution with a shared disk, as explained in a later section of this book.

- Use a physical disk in your virtual machine.

This is considered to be a configuration for advanced users. It allows you to use a disk partition from your existing physical disk, from within a virtual machine. The advantage is that it is the fastest type of disk access you can obtain for your virtual machine, but the disadvantage is that you need to partition your hard disk just as you would with a multi boot PC. Also, you will not be able to save the virtual machine easily with its configuration and disk files into an archive for back-up. In addition, it can not be used for future installations based on the same virtual machine copy.

It could be a useful installation if you have a dual boot PC, because you can start your extra operating system from the boot loader or from within a virtual machine.

Tip: I recommend the type of virtual disk that grows dynamically (the default selection when creating new virtual machines). It does not take up too much hard disk space, the performance is acceptable, and it is very easy to create an archive of a virtual machine by just copying the files to a safe location.

## 2.7 Networking Options for your Virtual Machines

Nowadays, all computers as well as your virtual machines come with a network adapter. It is important to know what types of networking you can use, because choosing the wrong type can prevent you from accessing your services in the virtual machines. It can also have undesired effects on your existing network.

In general, you have two types of networking options available: bridged and host-only.

### Bridged networking

This is the default type of networking that is selected when you create your virtual machine. It allows your guest operating system to communicate with the physical Ethernet network that your host is also using. The virtual machine has its own MAC address (a unique address for every networked machine) and will need to have its own IP address that it will either receive automatically from your DHCP server or that you will manually configure.

Accessing the network (and via that, the Internet) is very simple and straightforward. You must of course be aware that everything that you run inside your virtual machine will be accessible from the network. Therefore, installing a server of some sort (Domain Controller, DHCP server) will have serious implications for other users on your network. Unless if the plan was to run these services inside of the virtual machine in the first place. Just be aware of this, because you would not be the first one to run an extra DHCP server at a customer site, after accidentally running the wrong virtual machine.

### Host-only networking

If your virtual machines do not have to communicate with the network, or if you want to prevent this because you want to test network services that may not leak out onto the network, you can select this type of networking. All network traffic will be handled by an internal VMware process and nothing will leave your host PC. Virtual machines will be able to communicate with each other, and by using the virtual host-only adapter, your host operating system can also communicate with the guests. VMware comes with a DHCP service for your host-only network. The VMware manual describes how to use and configure this in detail.

### What networking option to use

If you will be running a simple workstation with Windows or Linux, then your best choice is bridged networking. You can access the network and, if available, the Internet, and update the machines with the latest patches.
