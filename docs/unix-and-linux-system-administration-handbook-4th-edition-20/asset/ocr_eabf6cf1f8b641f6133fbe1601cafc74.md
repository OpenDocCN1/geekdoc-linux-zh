# Xen guest installation with virt-install

993

Similarly, virtual network interfaces (aka VIFs) can be set up in multiple ways.
The default is to use bridged mode, in which each guest domain is a node on the
same network as the host. Routed and NAT modes configure guest domains to
a a private network, accessible to each other and domain 0 hidden from the
rest of the network. Advanced configurations include bonded network interfaces
and VLANs for guests on different networks. If none of these options fit the bill,
Xen scripts are customizable to meet almost any unique need.

# Xen guest installation with virt-install

One tool for simple guest installation is **virt-install**, bundled as part of Red Hat’s **virt-manager** application. **virt-install** is a command-line OS provisioning tool. It accepts installation media from a variety of sources, such as an NFS mount, a physical CD or DVD, or an HTTP location.

For example, the installation of a guest domain might look like this:

```
redhat5 sudo virt-install -n chef -f /vm/chef.img - http://example.com/myos-r 512 --nographics
```

This is a typical Xen guest domain with the name "chef," a disk VDM of /vm/chef.img, and installation media obtained through HTTP. The instance has 512MIB of RAM and no Windows-based graphics support during installation. **virt-install** downloads the files needed to start the installation and then kicks off the installer process.

You'll see the screen, and you'll go through a standard text-based installation, including network configuration and package selection. After the installation completes, the guest domain reboots and is ready for use. To disconnect from the guest console and return to dom0, type <Control->.

See page 1138 for more details on VNC.

It's worth noting that although this incantation of **virt-install** provides a text-based installation, graphical support through Virtual Network Computing (VNC) is also available.

The domain's configuration is stored in **/etc/xen/chef**. Here’s what it looks like:

```
name = "chef"
uuid = "a8520f4a-d11b-d4f7-9239b1d0d051"
maxmem = 512
memory = 512
vcpus = 1
bootloader = "/usr/bin/pygrub"
on_poweroff = "destroy"
on_reboot = "restart"
on_crash = "restart"
vfb = [ "tap:io/vm/chef.disk.xvda,w" ]
vif = "mac=00:16:3e:1e:57:79,bridge=xenbr0"

```

+   3. Install the python-virtvirt package for virt-install support on Ubuntu.