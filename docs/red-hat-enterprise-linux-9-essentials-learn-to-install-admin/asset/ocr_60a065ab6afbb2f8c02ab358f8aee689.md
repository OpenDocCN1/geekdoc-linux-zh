# Creating a RHEL 9 KVM Networked Bridge Interface

Similarly, when creating a new virtual machine using the virt-manager tool, the bridge will be available within the Network selection menu:

![](bbox=[0.32, 0.12, 0.63, 0.39])

Figure 25-3

To modify an existing virtual machine so that it uses the bridge, use the virsh edit command. This command loads the XML definition file into an editor where changes can be made and saved:

```
# virsh edit GuestName
```

By default, the file will be loaded into the vi editor. To use a different editor, change the $EDITOR environment variable, for example:

```
# export EDITOR=gedit
```

To change from the default virtual network, locate the <interface> section of the file, which will read as follows for a NAT-based configuration:

```
<interface type='network'>
    <mac address='<your mac address here>'/>
    <source network='default'/>
    <model type='virtio'/>
    <address type='pci' domain='0x0000' bus='0x01' slot='0x00' function='0x0'/>
</interface>
```

Alternatively, if the virtual machine was using a direct connection, the entry may read as follows:

```
<interface type='direct'>
    <mac address='<your mac address here>'/>
    <source dev='enol' mode='vepa'/>
    <model type='virtio'/>
    <address type='pci' domain='0x0000' bus='0x01' slot='0x00' function='0x0'/>
```

To use the bridge, change the source network property to read as follows before saving the file:

```
<interface type='network'>
    <mac address='<your mac address here>'/>
```