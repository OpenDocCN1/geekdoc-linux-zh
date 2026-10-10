When you create a virtual guest, you want to pass it the same information you entered when you used the Virtual Machine Manager window. Before you begin you need a few things in place. Here’s what I did for the example below:

+   Create a storage volume called myfedora.qcow2 (making sure it is large enough to hold the operating system being installed).

+   Get an install CD or DVD (or simply an ISO image of an install CD or DVD). In this example, I inserted a Fedora 12 installation DVD in the first DVD drive ( /dev/cdrom ).

The following example created a system named fedora12-01 . It uses 512MB of RAM and has the default networking configuration (default, virtio). It reads the installation medium from the first CD drive and lets you watch the installation from a VNC window. Here’s what the virt-install command looks like (split over several lines for readability):

```
# virt-install --connect qemu:///system \
    --name fedora12-01 \
    --ram 512 \
    --disk path=/var/lib/libvirt/images/myfedora.qcow2 \
    --network network=default,model=virtio \
    --vnc \
    --cdrom /dev/cdrom

Starting install...
Creating domain...
```

A VNC window appears, allowing you to step through the installation process. Once the installation process is done, you can manage the new guest from the Virtual Machine Manager window or from the command line using virsh (as described later in this chapter).

There are lots of ways you can modify the virt-install command shown above. Here are a few examples:

+   **Installation media** — Instead of installing from CD or DVD ( - - cdrom /dev/cdrom ), you can choose the location of the medium in other ways. If you can find an Internet site that has the operating system you want, you can simply point to its URL. Here are some examples:

<table><tr><td><code>-location=/root/dvd.iso</code></td><td>Install from <code>dvd.iso</code> in <code>/root</code></td></tr><tr><td><code>-location=nfs:bighost:/var/ftp/pub/MYOS</code></td><td>Install from NFS share from <code>bighost</code></td></tr><tr><td><code>-location=http://server10/MYOS</code></td><td>Install from a directory on a Web server</td></tr><tr><td><code>-location=ftp://myftp/MYOS</code></td><td>Install from a directory on an FTP server</td></tr></table>

+   **Architecture** — Using - -arch=ARCH you can specify that the guest requires a non-native architecture. By default, the architecture of the host CPU is used.