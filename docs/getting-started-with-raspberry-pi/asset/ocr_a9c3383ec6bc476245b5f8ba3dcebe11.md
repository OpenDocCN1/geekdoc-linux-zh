# Line Disciplines

Line disciplines provide an elegant mechanism that lets you use the same serial driver to run different technologies. The low-level physical driver and the tty driver handle the transfer of data to and from the hardware, while line disciplines are responsible for processing the data and transferring it between kernel space and user space.

The serial subsystem supports 17 standard line disciplines. The default line discipline that gets attached when you open a serial port is N_TTY, which implements terminal I/O processing. N_TTY is responsible for “cooking” characters received from the keyboard. Depending on user request, it maps the control character to newline, converts lowercase to uppercase, expands tabs, and echoes characters to the associated VT. N_TTY also supports a raw mode used by editors, which leaves all the preceding processing to user applications. See Figure 7.3 in the next chapter, “Input Drivers,” to learn how the keyboard subsystem is connected to N_TTY. The example tty drivers listed at the end of the previous section, “TTY Drivers,” use N_TTY by default.

Line disciplines also implement network interfaces over serial transport protocols. For example, line disciplines that are part of the Point-to-Point Protocol (N_PPP) and the Serial Line Internet Protocol (N_SLIP) subsystems, frame packets, allocate and populate associated networking data structures, and pass the data on to the corresponding network protocol stack. Other line disciplines handle Infrared Data (N_IRDA) and the Bluetooth Host Control Interface (N_HCI).

# Device Example: Touch Controller

Let’s take a look at the internals of a line discipline by implementing a simple line discipline for a serial touch-screen controller. Figure 6.6 shows how the touch controller is connected on an embedded laptop derivative. The Finite State Machine (FSM) of the touch controller is a candidate for being implemented as a line discipline because it can leverage the facilities and interfaces offered by the serial layer.

![](bbox=[0.18, 0.53, 0.82, 0.86])