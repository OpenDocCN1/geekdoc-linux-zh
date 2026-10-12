# **System Group**

The `system` group consists of objects that provide generic information about the device or system on which the agent is running. Figure 6.2 presents the hierarchical view of the system group.

![](bbox=[0.18, 0.18, 0.58, 0.38])

**Figure 6.2** _The system group view._

The objects in this group are mostly self-explanatory. The `sysServices`, `sysUptime`, and `sysOR` prefixed objects require additional information. The `sysServices` object represents a seven-bit code that corresponds to the value of the combined services the device provides. Each bit within the code is associated with one of the layers of the OSI model and, if the device offers a service on a particular layer, then the bit for that layer is set. For example, consider a device that provides routing functions. The associated `sysServices` value for this device is 72. Table 6.2 contains a list of layers and associated services. The value of `sysServices` is the sum of the bit values, where the value of any particular bit is 2 raised to the power L-1 (where L is the layer). Thus, for a switch device that is a layer 1 and 2 device, we get

```
$2^{1-1} + 2^{2-1} = 3$
```

and/or an application server (layers 4 and 7), we get

```
$2^{4-1} + 2^{7-1} = 72$
```