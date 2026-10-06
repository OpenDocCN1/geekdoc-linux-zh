# 7.2 SLIP Implementation in the Linux Kernel

be able to actually transmit packets, to have an appropriate route (either automatically, by ifconfig, or by another user program).

The above steps are done in reverse order to tear down a SLIP connection. More specifically, ifconfig is used to deactivate the network device. Any route registered for this device is deleted automatically by the Linux kernel, so that no data can be sent over this network device. The user can then use the command ifconfig down to cause the routine sl1_close() to be invoked in the Linux kernel. This routine informs the driver that the network device was deactivated, but it does not free the relevant data structures just created. Subsequently, no more data can be sent or received over this SLIP device.

The SLIP line discipline might need to be terminated for several reasons: First, it is possible that a user program calls the system call close() or the Linux kernel calls the function tty_hang() to close a serial connection. In the latter case, the Linux kernel resets the line discipline of the relevant TTY device automatically to the standard V_TTY. Second, it can happen that the TTY device is switched to another line discipline by the function tty_set_linidisc(). Each of these cases invokes the routine slip_close() in the SLIP driver. This routine does some cleanup (e.g., it decrements the usage counter of the SLIP module).

When the SLIP module is removed by the command rmmod slip, or automatically, the function cleanup_module() is invoked. For all, this ensures that all open SLIP connections are closed by the function tty_hang() and that all SLIP network devices are removed. Subsequently, it deregisters the SLIP TTY line discipline by calling tty_register_1idisc (N_SLIP, NULL). After, the SLIP TTY line discipline is no longer known in the system, and user programs can no longer use it.

# 7.2.7 Transmitting IP Packets

To transmit an IP packet, the IP layer invokes the function sl1_encaps() and passes an sk_buffer structure to this function. This function uses the function slip_esc() to do character stuffing and marking packet boundaries. By Section 7.1.1), the converted packet is in the transit buffer, and the pointer xhead points to the first of bytes.

To output data to the TTY device, sl1_encaps() invokes the write() routine of the relevant driver. This routine returns the number of bytes that can be transmitted in one shot. Subsequently, the xleft variable is set to the number of bytes still missing, and the xhead pointer points to the first of these bytes.

Because the function sl1_encaps() has the flag TTY_DO_WAKEUP, the TTY driver invokes the function slip1_write_wakeup() as soon as it has announced the number of bytes. Next, the function slip_write_wakeup() tries to transmit the remaining xleft bytes, starting from the position xhead returns the number of bytes to be actually transmitted, which causes xhead and xleft to be adapted accordingly. This process is repeated until the complete IP packet has been transmitted successfully, so that xleft equals null.