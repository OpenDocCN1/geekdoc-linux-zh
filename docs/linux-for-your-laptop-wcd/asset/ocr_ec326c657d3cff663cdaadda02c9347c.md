This sets up your parallel port using the specified I/O address and IRQ. You can then check your kernel messages:

```
$ dmesg
```

```
...
```

```
parport0: PC-style at 0x378, irq 7 [SPP,ECP,PCFPPS2]
```

This shows that the port has been initialized. Next, use insmod to load PLIP support and create your PLIP device:

```
$ insmod plip timed=1
```

The timed option instructs plp.o to avoid other I/O addresses or IRQs in use. You can then check for kernel output to see if the device was created:

```
$ dmesg
```

```
...
```

```
plip0: Parallel port at 0x378, using IRQ 7
```

Note that the parallel-port device returned (in this example, plp0). You can then use the ifconfig command to bring up the plip interface on each computer (and also to perhaps set the device netmask and so on). For example, on ComputerA, you would use this:

```
$ ifconfig plip0 ComputerA pointopoint ComputerB up
```

and on ComputerB you would use this:

```
$ ifconfig plip0 ComputerB pointopoint ComputerA up
```

You can then check the interface on each:

```
$ ifconfig plip0
```

```
plip0 Link encap:Ethernet HWaddr FC:PC:C0:A8:02:26 inet addr:192.168.2.38 P-t-P:192.168.2.30 Mask:255.255.255.255 UP POINTOPOINT RUNNING NOARP MTU:1500 Metric:1 RX packets:0 errors:0 dropped:0 overruns:0 frame:0 TX packets:0 errors:0 dropped:0 overruns:0 carrier:0 collisions:0 txqueuelen:10 Interrupt:7 Base address:0x378
```

You can then try to ping, telnet, or ftp to the other computer. Problems you might encounter include bad cables and incompatible parallel ports. To bring down the connection, use the ifconfig command like this:

```
$ ifconfig plip0 down
```