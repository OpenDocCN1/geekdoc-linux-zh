```
bash> irattach /dev/ttyS1 -s
```

Verify that IrDA kernel modules (*irda.ko, sir_dev.ko*, and *ir tty_sir.ko*) are loaded and that the *irda_sir_wq* kernel thread is running. The *irda0* interface should also have made an appearance in the *ifconfig* output. The *-s* option to *irattach* triggers a search for IR activity in the neighborhood. If you slide the laptops such that their IR transceivers lie within the range cone, they will be able to spot each other:

```
bash> cat /proc/net/irda/discovery

nickname: localhost, hctl: 0x4400, saddr: 0x55529048, daddr: 0x8fefb350
```

The other laptop makes a similar announcement, but with the source and destination addresses (*saddr* and *daddr*) reversed. You may set the desired communication speed using *stty* on *ttyS1*. To set the baud rate to 19200, do this:

```
bash> stty speed 19200 < /dev/ttyS1
```

The easiest way to cull IR activity from the air is by using the debug tool, *iradump*. Here's a sample dump obtained during the preceding connection establishment, which shows the negotiated parameters:

Code View:

```
bash> iradump -i irda0
...
22:05:07.831424 snrm:cmd ca=fe pf=1 6fb7ff33 > 2c0ce8b6 new-ca=40
LAP QoS: Baud Rate=19200bps Max Turn Time=500ms Data Size=2048B Window Size=7 Add BOFS=0 Min Turn Time=5000us Link Disc=12s (32)
22:05:07.987043 uarjsp ca=40 pf=1 6fb7ff33 < 2c0ce8b6
LAP QoS: Baud Rate=19200bps Max Turn Time=500ms Data Size=2048B Window Size=7 Add BOFS=0 Min Turn Time=5000us Link Disc=12s (31)
...
```

You can also obtain debug information out of the IrDA stack by controlling the verbosity level in * /proc/sys/net/irda/debug*.

To set the laptops in FIR mode, dissociate *ttyS1* from the native serial driver and instead attach it to the NSC FIR driver, *nsc-irc.ko*:

```
bash> setserial /dev/ttyS1 uart none
bash> modprobe nsc-irc dongle_id=0x09
bash> irattach irda0 -s
```

*dongle_id* depends on your IR hardware and can be found from your hardware documentation. As you did for SIR, take a look at * /proc/net/irda/discovery* to see whether things are okay thus far. Sometimes, FIR communication hangs at higher speeds. If *iradump* shows a communication freeze, either put on your kernel hacking hat and fix the code, or try lowering the negotiated speed by tweaking * /proc/sys/net/irda/max_baud_rate*.

Note that unlike the Bluetooth physical layer that can establish one-to-many connections, IR can support only a single connection per physical device at a time.