```
lo Link encap:Local Loopback
inet addr:127.0.0.1 Mask:255.0.0.0
UP LOOPBACK RUNNING MTU:3924 Metric:1
RX packets:359 errors:0 dropped:0 overruns:0 frame:0
TX packets:359 errors:0 dropped:0 overruns:0 carrier:0
collisions:0 txqueuelen:0
```

When used with the interface name, the `ifconfig` utility can `down` or `up` the network interface. The `down` command is used to disable the network interface while the `up` command is used to enable the interface. This capability can be useful when removing the system from the network for maintenance and for reinitializing the network configuration. Other options that can be configured using the `ifconfig` utility include IP address, broadcast address, netmask address, and adapter settings. `ifconfig` is the primary command used when making changes to the network configuration on a system.

The `ifconfig` utility is used with the following syntax and the options shown in Table 15-7.

```
ifconfig *interface options*
```

| **Table 15-7 Options Used with ifconfig** | | | | | | | | | |
|---|---|---|---|---|---|---|---|---|---|
| **Option** | **Use** | | | | | | | | |
| `up` | Used to activate the specified interface. | | | | | | | | |
| `down` | Used to deactivate the specified interface. | | | | | | | | |
| `netmask ADDRESS` | Specifies the *ADDRESS* used for the subnet mask. | | | | | | | | |
| `ADDRESS` | Specifies the *ADDRESS* used for the IP address. | | | | | | | | |
| `irq ADDRESS` | Specifies the IRQ *ADDRESS* used by the interface. | | | | | | | | |
| `io_addr ADDRESS` | Specifies the IO *ADDRESS* used by the interface. | | | | | | | | |
| `media TYPE` | Specifies the media *TYPE* used by the interface, such as 10Base-T, 100Base-T, and so on. | | | | | | | | |
| `mem_start ADDRESS` | Specifies the start *ADDRESS* for the shared memory address used by the interface. | | | | | | | | |

Following is an example of using the `ifconfig` utility to disable the `eth0` interface, to change the IP address to 10.254.90.153, to assign the netmask of 255.255.255.224 to the `eth0` interface, and to enable the `eth0` interface.