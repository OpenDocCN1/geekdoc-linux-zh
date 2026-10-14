Server section later in the chapter as that product doesn't require those extensions.

# Enable Support in BIOS

Once you have confirmed that your server will support KVM, you still will probably need to enable those extensions in your BIOS. Each BIOS is different, but reboot the machine and look for a section of the BIOS settings that includes processor settings or perhaps advanced settings and make sure that virtualization extensions are enabled.

# Install KVM Packages

Once the BIOS is all set, boot back into your server and install all of the packages you will need for KVM:

```
$ sudo apt-get install qemu-kvm libvirt-bin ubuntu-vm-builder
```

In addition to the KVM software and necessary libraries, this group of packages will also provide you with the virsh command-line tool you will need to manage your VMs. This will also install the ubuntu-vm-builder script, which makes spinning up new Ubuntu VMs incredibly easy.

Along with the root user you will probably want to set up at least one other user on the system who can directly manage VMs. To do this you simply need to add that user to the libvirtd group:

```
$ sudo adduser username libvirtd
```

Replace username with the name of your user. Note that you will have to log out and log back in for the group changes to take effect. Once you log back in, run the groups command and make sure that libvirtd is among your user's list of groups. At this point you are ready to test whether KVM is functioning and your user can manage it, so run the following virsh command:

```
$ virsh -c qemu:///system list
Connecting to uri: qemu:///system
Id Name State
-------------------------
```