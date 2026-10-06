
## 7.2 SLIP Implementation in the Linux Kernel

one (where the device is first reset to the standard line discipline N_TTTY by the Linux kernel) and when the TTY device itself is closed.

The function read() is called when a program wants to read data from the TTY device.

The function write() is called when a program wants to send data to the TTY device.

The function ioctl() is called when a program uses the system call ioctl() to change the configuration of the TTY line discipline or of the actual TTY device, but only provided that the higher-layer generic driver for TTY devices was unable to process the ioctl() call (as is the case, for example, when the device switches to another TTY line discipline).

The following functions are called from "below" (i.e., from the actual driver of the TTY device):

The function receive_buf() is called when the device driver has received data and wants to forward this data to the higher-layer program (i.e., to the driver of the TTY line discipline in this case). The parameters passed include the address and length of data.

The function receive_room() is called by the device driver to request the maximum number of bytes that the TTY line discipline can accept with receive_buf(). The function write_wakeup() optionally be called by the device driver as soon as it has finished sending a data block and is ready to accept more data. However, this happens only that it has been explicitly requested by the flag TTY_DO_WRITE_WAKEUP <linux/tty.h>.

### 7.2.2 General Procedure

The lifetime of a SLIP connection under Linux consists of the following phases; the sections below will explain how they are implemented in the Linux kernel:

- 1. Initialize the SLIP driver: the driver is initialized either when the system boots or when the driver module slip.o is loaded. At the same time, it registers the new TTY line discipline SLIP.
- 2. Establish the connection: A user program (e.g., dip or splatch) uses a modem connected to a serial interface (e.g., /dev/ttyS0) to dial to an Internet provider, and switches the TTY line discipline of this serial interface to SLIP. At the same time, the SLIP operating mode (e.g., CSLIP or SLIP6) must be correctly set.
- 3. Activate and configure the network device: Once the TTY line has been switched to SLIP, a new network device is available, and the name of this device begins with "sl" (e.g., s10). ifconfig then be used to activate and configure this network device (e.g., by assigning valid IP addresses to both ends of the SLIP connection).
- 4. Exchange data: As soon as the network device has been configured correctly, the SLIP connection is available for sending IP packets.
- 5. Deactivate the network device: Before the SLIP connection is torn down, the network device has to be deactivated by ifconfig.

![](img/5a25b942ec3329b8799f2b5f0de56f6160_0)

- 6. Tear down the connection: The user program (dip or splatch) separates the underlying modem connection, which causes the network device to be deregistered.
- 7. Deinitialize the SLIP driver: As soon as the driver module slip.o has been removed from the Linux kernel, it frees its memory and undoes the registration of the SLIP TTY line discipline.

### 7.2.3 Functions and Data Structures

The files drivers/net/slip.c and drivers/net/slip.h contain the source code for the SLIP implementation in the Linux kernel. Compression of IP packets by the Jacobson method is implemented in drivers/net/slip.c. However, this implementation will not be discussed in detail.

The SLIP driver represents each SLIP connection by a slip structure. This structure includes pointers to the net_device structure of the relevant SLIP device and to the tty_struct structure of the underlying TTY device (See Figure 7-4). The structure includes buffer pointers and counters to send and receive data. In addition, it stores the SLIP mode (e.g., CSLIP or SLIP6). In total, the slip structure consists of the following fields:

```c
struct slip {
```

- **tty**: points to a structure of the type tty_struct, which represents the TTY device allocated to this SLIP channel. This structure also includes a tty_ldisc structure with the TTY line discipline currently active (in this case, naturally SLIP).

![](img/5a25b942ec3329b8799f2b5f0de56f6161_0)

- **dev**: points to the net_device structure with the data of the network device allocated to the SLIP connection.
- **mtu**: is the MTU (Maximum Transmission Unit) of the SLIP connection, which is additionally stored in the net_device structure.
- **mode**: specifies the active SLIP operating mode (e.g., SL_MODE_SLIP, SL_MODE_CSLIP, or SL_MODE_SLIP6).
- **rbuf**: points to the receive buffer, which is used to buffer data incoming over the TTY device.
- **count**: is the number of data bytes currently present in the receive buffer.
- **xbuf**: points to the transmit buffer, which buffers data ready for output over the TTY device.
- **xhead**: points to the first character in the transmit buffer that has yet to be sent.
- **xlen**: specifies the number of bytes still waiting in the transmit buffer (from xhead).

![](img/5a25b942ec3329b8799f2b5f0de56f6162_0)

FIGURE 7-5 Functions of the SLIP implementation and their integration in the Linux kernel.

gives an overview of the functions discussed below. The following section also explains their interplay with other parts of the Linux kernel.

```c
slip_init_dev() drivers/net/slip.c
```

This function is called by init_module() when the SLIP module is loaded, and it uses the tty_register_ldisc() to register the SLIP TTY line discipline with the Linux kernel.

```c
slip_open() drivers/net/slip.c
```

This function is invoked by the function pointer open() in the tty_ldisc structure as soon as a user program wants to switch a TTY device to the SLIP line discipline. It reserves memory for the transmit and receive buffers and registers the new network device for the SLIP connection with the Linux kernel.

```c
slip_init() drivers/net/slip.c
```

This function is invoked by the Linux kernel whenever a new network device is registered, and it does a complete initialization of the network device and the appropriate net_device structure.

```c
slip_open() drivers/net/slip.c
```

This function is invoked by the function pointer open() of the net_device structure as soon as the SLIP network device is activated (e.g., by the command ifconfig).

```c
slip_close() drivers/net/slip.c
```

This function is invoked by the function pointer stop() of the net_device structure as soon as the SLIP network device is deactivated (e.g., by the command ifconfig down).

```c
slip_close() drivers/net/slip.c
```

This function is invoked by the function pointer close() of the tty_ldisc structure whenever the underlying TTY device is switched from the SLIP line discipline to another line.

```c
cleanup_module() drivers/net/slip.c
```

This function is invoked whenever the SLIP module is removed. Among other things, it ensures that all buffers are freed and all SLIP network devices are deregistered. Finally, the registration of the SLIP TTY line discipline with the Linux kernel is removed by calling tty_register_ldisc(N_SLIP, NULL).

### slip_xmit()

```c
drivers/net/slip.c
```

This function is invoked by the IP layer, which uses the function pointer hard_start_xmit() of the net_device structure to output an IP packet over the SLIP network device. The actual work is delegated to the function slip_encaps().

### slip_encaps()

```c
drivers/net/slip.c
```

This function is invoked by slip_xmit(). As explained in section 7.1, it converts the IP packet into a byte sequence. Depending on the SLIP operating mode (CSIP, etc.), other functions may be called in addition (e.g., the function slip_esc()). Subsequently, slip_encaps() invokes the write() of the underlying TTY driver, which eventually sends the built byte sequence previously created over the TTY device.

### slip_esc()

```c
drivers/net/slip.c
```

This function is invoked by slip_encaps() and does the character smashing described in Section 7.1.1. A similar function called slip_esc6() exists for the SLIP operating mode SLIP6, which additionally divides the data into 6-bit chunks and converts it into printable characters.

### slip_write_wakeup()

```c
drivers/net/slip.c
```

This function is invoked by the underlying TTY driver over the function pointer_write_wakeup() of the tty_ldisc structure (see Section 7.2.1) as soon as the TTY device is ready to accept more data. (Also See Section 7.2.7).

### slip_receive_room()

```c
drivers/net/slip.c
```

This function is invoked by the underlying TTY driver over the function pointer_receive_room() of the tty_ldisc structure and simply returns the value 65536, because the SLIP implementation can process a maximum of 65536 bytes per call of slip_receive_buf().

### slip_receive_buf()

```c
drivers/net/slip.c
```

This function is invoked by the underlying TTY driver to transfer data from the TTY device to the SLIP driver. receive_buf() of the tty_ldisc structure. The function slip_unesc() (slip_unesc6()), for the SLIP6 operating mode is invoked to convert the incoming byte stream back into IP packets.

### slip_unesc()

```c
drivers/net/slip.c
```

This function is invoked by slip_receive_buf(): it converts the incoming byte stream into IP packets, using the method described in Section 7.1.1.
