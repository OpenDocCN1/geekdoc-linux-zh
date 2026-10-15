# Objective 7 Use the hwup Command

The command hwup is used by udev to load driver modules and to initialize devices. In this objective, you learn how to use this command and how to interpret the corresponding configuration files.

To start a device, hwup is called with a hardware description as argument. The hardware description is a unique identifier for a specific device in the system. The following is an example hwup command line:

```
hwup bus-pci-0000:02:08.0
```

The device description consists of the following components:

+   - **bus.** This determines that the device is identified by the bus it is connected to.
+   - **pci.** This indicates that the device is connected to the PCI bus.
+   - **0000:02:08.0.** This is the address of the device in the PCI bus.

You can display the PCI address of a device with the lspci command, as in the following example:

```
...
0000:02:08.0 Ethernet controller: Intel Corp. 82801BD
PRO/100 VE (LOM) Ethernet Controller (rev 81)
...
```

As you can see, with the command hwup bus-pci-0000:02:08.0, the ethernet controller with the PCI adress 0000:02:08.0 would be started.

The command hwdown <hardware_description> can be used to stop a device. hwdown is a link to hwup and not a separate command.