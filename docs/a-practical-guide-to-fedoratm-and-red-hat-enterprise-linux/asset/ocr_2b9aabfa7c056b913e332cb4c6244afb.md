662 CHAPTER 17 SETTING UP VIRTUAL MACHINES LOCALLY AND IN THE CLOUD

# # IMPLEMENTATIONS

**libvirt** Many VM platforms, including QEMU, KVM, Xen, and VMware, can take advantage of on the libvirt¹ library and management tool that provides a consistent interface to create, monitor, and control VMs. While libvirt is not usually required, it can make the job of an administrator easier.

**Xen** Xen (www.cl.cam.ac.uk/research/srg/netos/xen, xenproject.org, and wiki.xen.org/wiki/Fedora_Host_Installation), which was created at the University of Cambridge and is now being developed in the open-source community, is an open-source hypervisor. Xen introduces minimal performance overhead compared with running each of the operating systems natively.

**VMware** VMware, Inc. (www.vmware.com) offers VMware Player, a free, downloadable, proprietary product you can install and run as an application under Fedora/RHEL. See page 671. VMware also offers ESXi, a hypervisor that runs directly on a machine (bare metal) without the need for an underlying operating system.

**KVM** KVM (the Kernel-based Virtual Machine; www.linux-kvm.org) is an open-source hypervisor that runs as part of the Linux kernel. See page 663.

**QEMU** QEMU (Quick EMUlator; wiki.QEMU.org), written by Fabrice Bellard, is an open-source hypervisor that runs as a user application with no CPU requirements. It can run code written for a different CPU than that of the host machine. See page 663.

**GNOME Boxes** The gnome-boxes utility (live.gnome.org/Boxes) is a simple although powerful GUI front end to libvirt that is designed to be run by end users. See the next section.

**VirtualBox** VirtualBox (www.virtualbox.org) is a VM developed by innotek GmbH, which was purchased by Sun Microsystems (now Oracle). It has been open source since version 4.

**virt-manager** The virt-manager utility is a GUI front end to libvirt that manages VMs. It typically manages QEMU/KVM VMs, although it can manage many different types of VMs. See page 665.

# ## gnome-boxes

The gnome-boxes utility, also called GNOME Boxes (live.gnome.org/Boxes), can connect to a VM or a remote system. It has a deceptively simple interface and can automatically detect VMs and perform an untended installation of a VM running any one of several different operating systems. It is not as powerful as virt-manager (page 665), which is designed for use by a system administrator, but it is very easy to use and convenient if you want to test a system quickly or if you do not want to get involved in the details of setting up a VM. Both gnome-boxes and virt-manager use the libvirt library and QEMU. You might need to enable hardware virtualization

1. Visit libvirt.org and access.redhat.com/site/documentation/en-US/Red_Hat_Enterprise_Linux/6/html/Virtualization_Getting_Started_Guide/sec_libvirt-libvirt-tools.html.