gdb responds by displaying this informational message and issuing the standard remote continue command instead.

# 14.3.1 gdb Remote Serial Protocol

gdb includes a debug switch that enables us to observe the remote protocol being used between gdb on a development host and the target. This can be very useful for understanding the underlying protocol, as well as troubleshooting targets that exhibit unusual or errant behavior. To enable this debug mode, issue the following command:

```
(gdb) set debug remote 1
```

With remote debugging enabled, it is instructive to observe the continue command in action and the steps taken by gdb. Listing 14-5 illustrates the use of the continue command with remote debugging enabled.

# Listing 14-5

cont/inuse Remote Protocol Example

```
(gdb) c
Continuing.
Sending packet: $mC000000,4#80...Ack
Packet received: c022d200
Sending packet: $mC000000,4:7d821008#0...Ack
Packet received: OK
Sending packet: $mC0016de8,4#f8...Ack
Packet received: 38600001
Sending packet: $mC0016de8,4:7d821008#e0...Ack
Packet received: OK
Sending packet: $mC005bd5c,4#23...Ack
Packet received: 38600001
Sending packet: $mC005bd5c,4:7d821008#0b...Ack
Packet received: OK
Sending packet: $mC021a488,4#c8...Ack
Packet received: 4bffbad
Sending packet: $mC021a488,4:7d821008#b0...Ack
Packet received: OK
Sending packet: $c#63...Ack
<< program running, gdb waiting for event
```

Although it might look daunting at first, what is happening here is easily understood. In summary, gdb is restoring all its breakpoints on the target. Recall from Listing 14-3 that we entered two breakpoints, one at panic() and one at sys_sync(). Later in Listing 14-4, we added a third breakpoint at yosemite_setup_arch(). Thus, there are three active user-specified breakpoints.