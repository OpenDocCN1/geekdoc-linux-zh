# 140 Chapter 7 The Serial-Line Internet Protocol (SLIP)

gives an overview of the functions discussed below. The following section also explains their interplay with other parts of the Linux kernel.

```
slip_init_ctrl_dev()                               drivers/net/slip.c
```

This function is called by init module() when the SLIP module is loaded, and it uses the tty_register_ldisc() to register the SLIP TTY line discipline with the Linux kernel.

```
slip_open()                               drivers/net/slip.c
```

This function is invoked by the function pointer open() in the tty_ldisc structure as soon as a user program wants to switch a TTY device to the SLIP line discipline. It reserves memory for the transmit and receive buffers and registers the new network device for the SLIP connection with the Linux kernel.

```
s1_init()                                     drivers/net/slip.c
```

This function is invoked by the Linux kernel whenever a new network device is registered, and it does a complete initialization of the network device and the appropriate net_device structure.

```
s1_open()                                     drivers/net/slip.c
```

This function is invoked by the function pointer open() of the net_device structure as soon as the SLIP network device is activated (e.g., by the command ifconfig).

```
s1_close()                                    drivers/net/slip.c
```

This function is invoked by the function pointer stop() of the net_device structure as soon as the SLIP network device is deactivated (e.g., by the command ifconfig down).

```
slip_close()                                   drivers/net/slip.c
```

This function is invoked by the function pointer close() of the tty_ldisc structure whenever the underlying TTY device is switched from the SLIP line discipline to another line.

```
cleanup_module()                                 drivers/net/slip.c
```

This function is invoked whenever the SLIP module is removed. Among other things, it ensures that all buffers are freed and all SLIP network devices are deregistered. Finally, the registration of the SLIP TTY line discipline with the Linux kernel is removed by calling tty_register_ldisc(N_SLIP, NULL).