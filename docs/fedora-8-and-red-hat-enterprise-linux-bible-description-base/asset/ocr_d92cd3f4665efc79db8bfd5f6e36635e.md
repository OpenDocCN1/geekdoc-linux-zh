# # Running applications virtually with Xen

Xen (www .xensource. com) is virtualization software that is included in Fedora. Using Xen, you can run multiple operating system instances within a running Fedora system. These operating systems, referred to as virtual machines, can not only run applications built specifically for those operating systems. They can also appear to the network as though they are running on completely different machines.

To demonstrate Xen features, the procedures in this section describe how to set up a virtual machine of Fedora that will run on an installed host Fedora system. Currently, to run other operating systems on Xen in Fedora, you need to supply an OS image, rather than build one from scratch as shown in the procedure below.

If you run into road blocks with Xen, there are places to get help. To ask questions about Xen, see the Fedora-Xen mailing list (www. redhat .com/mailman/listinfo/fedora-xen). Try the Xen Tools page (http://fedoraproject. org/wiki/Tools/Xen) for links to further information on Xen in Fedora.

You can find more information about how Xen works and what it is from the Xen Source Wiki (http://wiki. xensource. com/xenwiki). In particular, select the Xen FAQ link (for information on what Xen is) or the HowTos link (for links to the user manual and specialty HowTos).

# ## Before installing Xen

Xen requires a lot of resources to run. Each operating system instance (referred to as a guest operating system) will need almost the full amount of resources it would need to run separately. Therefore, before you begin, make sure your system has at least the following available:

+   - **RAM** — In general, your computer should have at least 256MB of RAM available for each guest you want to have, plus the amount of RAM required for the type of Fedora install you selected.
+   - **Hard Disk** — On top of what you need to install Fedora, you need the entire amount of disk space required by each operating system guest you installed. Of course, these amounts can vary greatly, with minimal server installs starting at around 600MB and average desktop installs typically starting at 2GB or 3GB.
+   - **Paravirtualization (PAE) support** — Your computer's CPU must support the PAE extension. Many laptops will not have PAE support. To see if your computer has PAE support, type the following:

```
# cat /proc/cpuinfo | grep pae
flags : fpu vme de pse tsc msr pae mca cx8 apic
mtrr pge mcm cxmmx fxsr syscal1
mmxext 3dnowext 3dnow up
```