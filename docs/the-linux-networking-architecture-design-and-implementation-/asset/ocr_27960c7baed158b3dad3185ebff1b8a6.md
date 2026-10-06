# 5.3 Network Drivers 109

+   * be the case if the chipset_init() call above just
* flushes out the tx queue and empties it.
*
* If instead, the tx queue is retained then the
* netif_wake_queue() call should be placed in the
* TX completion interrupt handler of the driver instead
* of here.

```
*/
if (!tx_full(dev))
    netif_wake_queue(dev);
}
```

# 5.3.5 Runtime set_config()

```
drivers/net/isa_skeleton.c
```

In certain situations, it may be necessary to change the configuration of the system resources used by a network adapter at runtime—for example, when the interrupt cannot be identified automatically, or when there are conflicts with other devices. The driver method set_config() can be used to manipulate the configuration of system resources (i.e., interrupt, DMA, etc.) at runtime.

When the current configuration is polled on the application level, then the irq, dma, base_addr, mem_start, and mem_end parameters can be read directly from the net_device structure. However, when one of these parameters has to be changed, then we need a driver-specific method to fetch the changes in the adapter. We will use the method set_config(), which allows us to change only the interrupt line, as an example to show how system resources can be changed in general.

The driver method set_config() is called when an application process invokes the ioctl() command SIOCSFMAP (Socket I/O Control Set Interface MAP). Beforehand, however, the process should read the current configuration by use of the ioctl(1) command SIOCGIFMAP (Socket I/O Control Get Interface MAP). The reason is that, when it wants to change a value, the other parameters should have the current values.

For both ioctl() commands, the system parameters are passed in a structure of type ifmap. The ifmap has the following fields, corresponding to the fields with the same names in the net_device structure.

```
struct ifmap {
    unsigned long mem_start;
    unsigned long mem_end;
    unsigned short base_addr;
    unsigned char irq;
    unsigned char dma;
    unsigned char port;
}
```

The method's return value is also used as return value for the ioctl() call. Drivers that don't implement set_config() return -EOPNOTSUPP.