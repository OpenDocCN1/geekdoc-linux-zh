# WHAT IS SO GOOD ABOUT LINUX?

+   - Sandboxes—A VM presents a sandbox—an area (system) that you can work without regard for the results of work or for the need to clean up.

+   - Snapshots—You can take snapshots of a VM and return the VM to the state it was in you took the snapshot simply by reloading the VM from the snapshot.

Xen, which was created at the University of Cambridge and is now being developed in the open-source community, is an open-source virtual monitor (VMM). A VM enables several virtual machines (VMs), each running an instance of a separate operating system, to run on a single computer. Xen isolates the VMs so that if one crashes it does not affect of the others. In addition, Xen introduces minimal performance overhead when compared with running each of the operating systems natively.

Using VMs, you can experiment with cutting-edge releases of operating systems and applications without concern for the base (stable) system, all on a single machine. You can also set up and test networks of systems on a single machine. Xen presents a sandbox, an area (system) that you can work without regard for the results of your work or for the need to clean up.

The Lucid release of Ubuntu supports Xen 3.3. This book does not cover the installation of Xen. See help.ubuntu.com/community/Xen for information on running Xen under Ubuntu. For more information on Xen, refer to the Xen home page at www.clam.ac.uk/research/srg/xen and to wiki.xensource.com/wiki.

VMware Inc. (www.vmware.com) offers VMware Server, a free, downloadable proprietary product you can install and run as an application under Ubuntu. VMware enables you to install several VMs, each running a different operating system, including Windows and Linux. VMware also offers a free VMware player allows you to run VMs you create with the VMware Server.

KVM The Kernel-based Virtual Machine (KVM; kvm.quadrant.net and libvirt.org) is an open-source VM and runs as part of the Linux kernel. It only works on systems based on the Intel VT (VMX) CPU or the AMD SVM CPU; it is implemented as the kvm, libvirt-bin, and ubuntu-vm-builder packages. For more information refer to help.ubuntu.com/community/KVM.

Qemu (bellard.org/qemu), written by Fabrice Bellard, is an open-source VMM that runs as an application with no CPU requirements. You can run code written for a different CPU than that of the host machine. For more information refer to https://help.ubuntu.com/community/Installation/QemuEmulator.

VirtualBox VirtualBox (www.virtualbox.org) is a VM developed by Sun Microsystems. If you want to run a virtual instance of Windows, you may want to investigate KVM (help.ubuntu.com/community/KVM) and VirtualBox.