```
<model type='virtio' heads='1' primary='yes'/>
<address type='pci' domain='0x0000' bus='0x00' slot='0x01' function='0x0'/>
</video>
<redirdev bus='usb' type='spicevmc'>
<address type='usb' bus='0' port='2'/>
</redirdev>
<redirdev bus='usb' type='spicevmc'>
<address type='usb' bus='0' port='3'/>
</redirdev>
<memballoon model='virtio'>
<address type='pci' domain='0x0000' bus='0x05' slot='0x00' function='0x0'/>
</memballoon>
<rng model='virtio'>
<backend model='random'>/dev/urandom</backend>
<address type='pci' domain='0x0000' bus='0x06' slot='0x00' function='0x0'/>
</rng>
</devices>
</domain>
```

This file defines a number of hardware settings that are used by this guest, such as the amount of RAM that it will have assigned to it, the number of CPU cores from the hypervisor that the guest will have access to, the hard disk image file that is associated with this guest (under the disk stanza), its display capabilities (via the SPICE protocol), and the guest's access to USB devices as well as emulated keyboard and mice input.

# ## Example Virtual Machine Disk Storage

This virtual machine's hard disk image resides at /var/lib/libvirt/images/rhel8. Here is the disk image itself on this hypervisor:

```
$ sudo ls -lh /var/lib/libvirt/images/rhel8
-rw------- 1 root root 5.5G Oct 25 15:57 /var/lib/libvirt/images/rhel8
```

The current size of this disk image consumes only 5.5 GB of space on the hypervisor. However, the operating system within this guest sees a 23.3 GB sized disk, as evidenced by the output of the following command from within the running virtual machine:

```
$ lsblk
NAME         MAJ:MIN RM   SIZE RO TYPE MOUNTPOINT
vda            252:0    0  23.3G  0 disk
└─vda1         252:1    0     1G  0 part /boot
```