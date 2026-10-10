```
```
}
/* ... */
```
```

Figure 4.5 continues to peel off more layers to get to the bottom of the device modeling. It illustrates the transitions that ripple through classes, kobjects, sysfs, and udev, which result in the generation of the /sys and /dev files listed previously.

# Figure 4.5. Tying the pieces of the device model.

![](bbox=[0.17, 0.25, 0.82, 0.7])

Look at the parallel port LED driver (Listing 5.6 in the section "Talking to the Parallel Port" in Chapter 5) and the virtual mouse input driver (Listing 7.2 in the section "Device Example: Virtual Mouse" in Chapter 7) for examples on creating device control files inside sysfs.

Another abstraction that is part of the device model is the *bus-device-driver* programming interface. Kernel device support is cleanly structured into buses, devices, and drivers. This renders the individual driver implementations simpler and more general. *Bus* implementations can, for example, search for drivers that can handle a particular device.

Consider the kernel's I²C subsystem (explored in Chapter 8, "The Inter-Integrated Circuit Protocol"). The I²C layer consists of a core infrastructure, device drivers for bus adapters, and drivers for client devices. The I²C