# Linux Administration: A Beginner's Guide

The KVM virtualization that we set up earlier used the management tools (virt-manager, virt-install, and so on) that were designed to work seamlessly on Fedora, Red Enterprise Linux (RHEL), and CentOS platforms. Here, we will run through a quick and dirty setup of KVM virtualization that should work with little modification on any Linux distro.

Specifically, we will look at how to set up KVM in a Debian-based distro, such as Ubuntu. The processor on our sample Ubuntu server supports the necessary CPU extensions. We will be installing on a host computer with an Intel-VT capable processor. The target virtual machine will be any recent copy of the desktop version of Ubuntu and will be installed using the ISO image downloaded from #releases.ubuntu.com.

Install the KVM and QEMU packages. On the Ubuntu server, type this:

+   Install the kvm-intel module:
`master@ubuntu-server:~ sudo apt-get -y install qemu-kvm`

+   Manually load the kvm-intel module:
`master@ubuntu-server:~ sudo modprobe kvm-intel`

> NOTE Loading kvm-intel module will also automatically load the required kvm module. On an AMD-based system, the required is instead called kvm-amd.

+   We are going to run KVM as a regular user, so we need to add our sample user (yyang) to the kvm system group:
`master@ubuntu-server:~ sudo adduser yyyang`

+   Log out of the system and log back in as the user yyang so that the new group membership can take effect.

+   Create a folder in the user's home directory to store the virtual machine, and change into that:
`master@ubuntu-server:~ mkdir -p /home/yyang/vms/`
`master@ubuntu-server:~ cd /home/yyang/vms/`

> NOTE libvirt and virt-manager have been ported for use on other Linux distributions. For example, installing virt-manager on a Debian-based distro like Ubuntu is as simple as running
`master@ubuntu:~ sudo apt-get install virt-manager`