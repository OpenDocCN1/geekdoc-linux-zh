# 86 Chapter 5 Network Devices

returns an error message; otherwise, the network device is simply appended to the end of the linked list dev_base, so that it is available for general use.

In addition, the state dev->state is set to LINK_STATE_PRESENT in register_netdevice(), and dev_init_scheduler() sets the scheduling process for the new network device to the standard FIFO mechanism. This method is also used to cause the function dev->watchdog_init() to initialize the timer to detect transmission problems (dev->watchdog_timer; see Section 5.3.4). However, this timer is not started before the network adapter is activated (dev_open(); see Section 5.2.2).

Finally, the network device obtains a new number (dev->index), and notifier_call_chain(&dev_chain, NETDEV_REGISTER, dev) calls all registered methods in the notification chain dev_chain.

```
unregister_netdevice()
```

unregister_netdevice(dev) removes the network device passed as parameter from the list of registered network devices (dev_base). If the network device is still in active state (IFF_UP), it is now closed by the driver function dev->close(). Subsequently, it is erased from the linked list dev_base and if it is not found, the function returns an error message.

Once the structure has been removed, unregister_netdevice(dev) synchronizes itself to the RT-RX software interrupt by the big reader BR_NETPROTO:LOCK. Subsequently, the queuing discipline is released by dev->shutdown(). And all registered functions in the notification chain netdev chain are informed about the NETDEV_UNREGISTER. Subsequently, the destructor of the network driver is called, if it exists. Only the most recent network drivers have destructors, so we check periodically whether existing references to the network device (dev->refcount) persist for older drivers to be able to remove the network device.

# 5.2.2 Opening and Closing Network Devices

The previous section described how a network device is registered; the current section explains how one can be activated and deactivated. With other device types in the Linux system, activating andactivating is referred to as opening and closing. To open and close a network device, the administrator can use the command ifconfig. It is used not to activate and deactivate network devices, but also to configure them. More specifically, this command is used to set protocol-specific parameters, such as addresses and subnet masks, and to modify interface parameters for the network adapter (hardware parameters).

In addition, ifconfig can be used to change the flags of a network device. The syntax of ifconfig and its options are listed in Appendix C.1. Naturally, before a network device is activated, it has to be registered.

Activating a Network Device When we use ifconfig address to activate a network device, ifconfig uses the ioctl() command SIOCSIFADDR (Socket I/O Control Interface ADDAddr) to allocate the specified address to the network device name. The handling routine for the INET address family is devinet_ioctl().