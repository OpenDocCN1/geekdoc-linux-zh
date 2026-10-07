![](bbox=[0.154, 0.105, 0.725, 0.368])

**Figure 14.3**nA simple breakdown of the Linux USB gadget functional layer.

Figure 14.3 provides a simple breakdown of the function layer of the gadget subsystem.

From Figure 14.3, you can infer that the functional layer consists of routines that decide the USB characteristics. One routine manages the USB descriptors, a set of routines manages the storage or mouse functionality that the USB device implements, and other routines interact with Linux file systems to export the internal data structure to user space as `gadgetfs`.

The other important framework of the functional layer is the composite driver framework, which is optional.

With the given infrastructure, you can build a composite device, supporting multiple functions. The composite infrastructure can support single configuration and multiconfiguration devices supporting multiple functions not necessarily having more than one function per configuration. Figure 14.4 illustrates the functional breakdown of the composite driver framework.

The composite framework provides methods to add configuration and functionalities and data structures to maintain them. The subsequent section concentrates only on the composite framework and the sequence of activity