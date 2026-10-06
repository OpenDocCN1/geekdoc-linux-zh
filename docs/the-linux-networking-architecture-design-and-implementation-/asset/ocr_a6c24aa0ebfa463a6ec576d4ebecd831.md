# 7.2 SLIP Implementation in the Linux Kernel 137

one (where the device is first reset to the standard line discipline N_TTX by the Linux kernel) and when the TTY device itself is closed.

The function read() is called when a program wants to read data from the TTY device.

The function write() is called when a program wants to send data to the TTY device.

The function ioctl() is called when a program uses the system call ioctl() to change the configuration of the TTY line discipline or of the actual TTY device, but only provided that the higher-layer generic driver for TTY devices was unable to process the ioctl() call (as is the case, for example, when the device switches to another TTY line discipline).

The following functions are called from "below" (i.e., from the actual driver of the TTY device):

The function receive_buf() is called when the device driver has received data and wants to forward this data to the higher-layer program (i.e., to the driver of the TTY line discipline in this case). The parameters passed include the address and length of data.

The function receive_room() is called by the device driver to request the maximum number of bytes that the TTY line discipline can accept with receive_buf(). The function write_wakeup() optionally be called by the device driver as soon as it has finished sending a data block and is ready to accept more data. However, this happens only that it has been explicitly requested by the flag TTY_DO_WRITE_WAKEUP <linux/tty.h>.

# 7.2.2 General Procedure

The lifetime of a SLIP connection under Linux consists of the following phases; the sections below will explain how they are implemented in the Linux kernel:

+   1. Initialize the SLIP driver: the driver is initialized either when the system boots or when the driver module slip.o is loaded. At the same time, it registers the new TTY line discipline SLIP.

+   2. Establish the connection: A user program (e.g., dip or splatch) uses a modem connected to a serial interface (e.g., /dev/ttyS0) to dial to an Internet provider, and switches the TTY line discipline of this serial interface to SLIP. At the same time, the SLIP operating mode (e.g., CSLIP or SLIP6) must be correctly set.

+   3. Activate and configure the network device: Once the TTY line has been switched to SLIP, a new network device is available, and the name of this device begins with "sl" (e.g., s10). ifconfig then be used to activate and configure this network device (e.g., by assigning valid IP addresses to both ends of the SLIP connection).

+   4. Exchange data: As soon as the network device has been configured correctly, the SLIP connection is available for sending IP packets.

+   5. Deactivate the network device: Before the SLIP connection is torn down, the network device has to be deactivated by ifconfig.

![](bbox=[0.015, 0.975, 0.045, 0.995])