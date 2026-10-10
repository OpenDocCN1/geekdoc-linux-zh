+   8.  **Host network** — Choose how would like your new virtual system to connect to the host network. In most cases, select Virtual network. However, you can also select a shared physical device (such as an Ethernet bridge or MAC address).

+   9.  **Allocate Memory** — Type a number representing the maximum number of megabytes of RAM you want to dedicate to this virtual machine and the amount you want to start with and click Forward. At least 256 megabytes of RAM are recommended. If you have more available, you should use more since it will improve performance. You can also select to use multiple virtual CPUs (1 is the default).

+   10. **Finish** — When all the information has been entered, a summary of the information you entered appears as shown in Figure 5-6. Click Finish. The new virtual machine should appear on the Virtual Machine Manager window. Select it and click Open.

+   11. **Start installation** — A virtual machine console should appear, ready to install your guest Fedora 7 installation.

+   12. **Install Guest** — Because you are installing a Fedora 7 guest on a Fedora 8 system, you can basically follow along the installation instructions in Chapter 2 of this book. For disk partitioning, you can instruct the installer to use the entire partition or you can create multiple partitions.

After Fedora is installed as a guest, you can open that virtual machine as you need it from the Virtual Machine Manager window. If you selected Ethernet bridging, and there is a DHCP server on your network, your virtual machine can be assigned its own IP address. So you can use tools in Fedora to access the Internet and update and get new software as needed.

To manage your virtual machines from the command line you can use the xm command. To see which virtual machines are currently available, type the following:

```
# xm list
Name    ID Mem VCPUs State Time
Domain-0  0 453  1 r---- 1675.5
Fedora    264   1 r---- 243.9
```

If you want to save a snapshot of your virtual machine, use the xm command to save it to a file. For example, to save a virtual machine named Fedora to /tmp/virt-save, you could type the following:

```
# xm save Fedora /tmp/virt-save
```

Later, to restore the virtual machine, you could type:

```
# xm restore /tmp/virt-save
```

For details on working with Xen virtual machines in Fedora, refer to the Fedora Xen Quickstart (http://fedoraproject.org/wiki/Docs/Fedora7VirtQuickStart).