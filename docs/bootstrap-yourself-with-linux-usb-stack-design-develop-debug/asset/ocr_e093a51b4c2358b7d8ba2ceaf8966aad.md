![](bbox=[0.0823, 0.1015, 0.7535, 0.3655])

**Figure 2.6** USB communication flow illustrating the endpoint, pipe, and client software relationship.

bus. One of the important pipes is the default control pipe, which is associated with Endpoint Zero and is available once the device is powered and has been reset. The host system software uses the default control pipe to identify and configure the device.

# ## ENUMERATION

The process of identifying the device and setting a unique address is referred as *bus enumeration*. The enumeration process is handled by the system software over the host and the USB logical layer on the device side. The enumeration process starts when a device is attached to the host and the device gets the power. The USB specification includes simple steps for enumeration.

+   1. The USB device is attached to the host, which receives an event indicating a change in the pipe's status. The USB device is in the powered state, and the port it is attached to is disabled.
2. The host queries about the change in the bus.
3. Once the host determines that a new device is attached, it waits for at least 100ms for the device to become stable after power, after which it enables and resets the port.