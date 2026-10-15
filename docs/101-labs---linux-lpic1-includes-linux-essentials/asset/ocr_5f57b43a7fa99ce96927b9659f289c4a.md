
# Task 2

In VirtualBox, make a clone of this VM. Boot it, access the Terminal, and run: `ip addr show`

Compare the results with the original VM. Are the IP address and MAC address the same, or were they automatically changed? (Depending on your settings, either could be the case.)

In a cloud scenario of multiple machines being cloned onto the same network, it is critical to make sure the network information is unique for each instance. This is also true of some security-related information, such as SSH host keys and the D-Bus machine ID.

# Task 3

Finally, it is important to understand that guest VM's must have certain features beyond a generic Linux installation to make them usable as VMs. To illustrate this, run:

```
lsmod | grep vbox
```

You may see several VirtualBox-related kernel modules, such as `vboxguest`, `vboxsf`, or `vboxvideo`, among others. Additionally, specific kernel configuration is required: `grep GUEST /boot/config*`

# Notes

Cloud-init is a package commonly used in cloud server environments to handle the unique per-server configuration on the first boot of an image deployment.
