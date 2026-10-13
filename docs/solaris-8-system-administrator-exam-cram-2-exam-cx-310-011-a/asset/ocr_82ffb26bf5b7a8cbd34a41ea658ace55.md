```
c0          scsi-bus   connected   configured   unknown
c0::rmt/0   tape       connected   configured   unknown
c1          scsi-bus   connected   configured   unknown
c1::dsk/c1t3d0  disk   connected   configured   unknown
#
```

You can disconnect a SCSI controller by using the **cfgadm -c disconnect AP_Id** command. For example, to disconnect the c1 controller, use the following command:

```
# cfgadm -c disconnect c1
#
```

Likewise, to connect the c1 controller, use the following command:

```
# cfgadm -c connect c1
#
```

Adding a SCSI device (such as a disk) requires the **cfgadm -x insert_device AP_Id** command. For example, to add a disk to the c0 controller on a SPARC system, use this command:

```
# cfgadm -x insert_device c0
Adding device to SCSI HBA: /devices/sbus@f1,0/SUNW,fas@0,8800000
This operation will suspend activity on SCSI bus: c0
Continue (yes/no)? y
SCSI bus quiesced successfully.
It is now safe to proceed with hotplug operation.
Enter y if operation is complete or n to abort (yes/no)? y
#
```

You can use similar **cfgadm** commands to replace (**cfgadm -x replace_device AP_Id**), remove (**cfgadm -x remove_device AP_Id**), configure (**cfgadm -c configure AP_Id**), or unconfigure (**cfgadm -c unconfigure AP_Id**) SCSI devices as needed. In addition, you can use the **cfgadm -t AP_Id** command to perform diagnostic tests on an attachment point.

# Hot-Plugging PCI Adapter Cards

The **cfgadm** command displays information about hot-plugging configurations and connects, disconnects, configures, and unconfigures PCI adapter cards.

Attachment point IDs (AP_Ids) for PCI devices are based on the PCI bus and slot. For example, slot 0 of PCI bus 1 has an AP_Id of pci1:hp0_slot0.