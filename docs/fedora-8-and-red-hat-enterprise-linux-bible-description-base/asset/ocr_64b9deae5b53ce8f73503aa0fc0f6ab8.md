+   - You need an Intel VT or AMD-\V processor (see the “Before Installing Xen” section for information on how to check for pae support),

Next, you want to install many of the same packages you installed for Xen. From Package Manager you can simply Browse to Base System → Virtualization and install all the optional packages. In particular, add the kvm and qemu packages to those needed by Xen (such as virt-manager).

Before proceeding, make sure that you booted to the regular kernel and not the Xen kernel (if the xen-kernel package is installed, both a regular and xen kernel should be available for you to boot from). Then run the following procedure to install a new guest operating system that will run using KVM and QEMU:

+   1. **Start KVM guest-install** — As root user from a Terminal window, type the following:
+      ```
+      # /usr/sbin/virt-manager
+      ```
+      The Virtual Machine Manager window appears.

+   2. **Create new guest** — Right-click localhost (qemu) and click New. When the Create a new virtual system pop-up appears, click Forward. You are asked to name your virtual system.

+   3. **Virtual machine name** — Type a name to represent this virtual machine and click Forward. Keep the name simple (one word, fairly short, and no special characters) because the name is used to represent the virtual machine in file names and on menus. You are asked the virtualization method.

+   4. **Virtualization method** — Choose Fully Virtualized. You can also choose to create a guest that uses a different CPU architecture (i686, X86_64, ppc, sparc, mips, or mipsel). You are asked to identify the location of the installation media.

+   5. **Installation media** — Type the location of an ISO image (you can browse for it) or the CD or DVD drive that has your installation media (such as a Fedora Install DVD) inserted. Also identify the type (generic, Linux, UNIX, Windows, or other) and variant (Fedora, Windows Vista, Sun Solaris, for example) of the operating system you are installing. You are asked to assign storage space.

+   6. **Assign storage space** — You can either identify a disk partition or create a virtual disk by identifying a file name and size. In either case, the storage area must be large enough to hold your installed guest operating system. You are asked to set up a network connection.

+   7. **Host network** — Identify either a virtual network or shared physical network device to provide network connectivity for your guest operating system. Next allocate memory and CPU.

+   8. **Allocate memory** — From the total memory amount shown on the screen, choose the amount of VM memory to use and the maximum amount to use. At least 256MB is recommended.