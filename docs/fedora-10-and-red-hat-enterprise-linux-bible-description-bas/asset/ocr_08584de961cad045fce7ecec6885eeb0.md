# Part II: Using Fedora and RHEL

You can find more information about how Xen works and what it is from the Xen Source Wiki (http://wiki.xource.com/wiki). In particular, select the Xen FAQ link (for information on what Xen is) or the HowTos link (for links to the user manual and specialty HowTos).

# Before installing Xen

Xen requires a lot of resources to run. Each operating system instance (referred to as a guest operating system) will need almost the full amount of resources it would need to run separately. Therefore, before you begin, make sure your system has at least the following:

+   **RAM** — In general, your computer should have at least 256MB of RAM for each guest you want to have, please the amount of RAM required for the type of Fedora you selected.

+   **Hard Disk** — On top of what you need to install Fedora, you need the entire amount of disk space required by each operating system guest you install. Of course, these amounts can vary greatly, with minimal server installs starting at around 600MB and average desktop installs typically starting at 2GB or 3GB.

+   **Paravirtualization (PAE) support** — Your computer's CPU must support the PAE extension. Many laptops will not PAE support. To see if your computer has PAE support, type the following:

In this example, PAE is supported. If it were not supported, nothing would be returned.

+   **Fully-virtualized guest support** — In order to run fully virtualized guests, you need Intel VT or AMD-V support, depending on your processor. Check your cpuinfo (as shown above) type grep vmx or svm (on Intel or AMD processors, respectively). If you see output, the program is supported.

+   **GRUB boot loader** — A final requirement of the setup is that GRUB be your boot loader. When you install Xen, it will automatically add itself to your GRUB boot loader as a secondary choice of operating system kernels that you can choose to boot.

# Installing Xen

To run Xen in Fedora, you need to install and boot from a specially configured kernel. Xen kernel packages are not installed by default with Fedora, so you have to either select them at install time or add them. Here's how to install the Xen packages you need: