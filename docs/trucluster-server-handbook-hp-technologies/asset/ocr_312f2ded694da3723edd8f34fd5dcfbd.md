```
# niffconfig -v
Interface: tu0, description: , status: UP, event: ALERT, state: GREEN
t1: 20, dt: 5, t2: 60, time to dead: 30, current_interval: 20, next time: 20
```

Figure 9-1 shows the niffmt to niffd communication path.

The niffmt thread checks the monitored interface every t1 seconds. If niffmt detects a connectivity problem, then it posts a sys.unix.hw.net.niff.alert event to EVM and then starts checking the monitored interface every dt seconds. The niffd daemon receives the sys.unix.hw.net.niff.alert event from EVM and begins generating traffic on the interface until it receives a sys.unix.hw.net.niff.down or sys.unix.hw.net.niff.up event. If t2 seconds elapse without the monitored interface's counters increasing, then the interface is marked as DEAD, and a sys.unix.hw.net.niff.down event is sent by niffmt.

# 9.1.1 NIFF Events

NIFF events are defined in /usr/share/evm/templates/sys/hw.net.evt. Below are the registered NIFF events:

```
# evmwatch -A -i -f "[name *.niff]" -t "[@priority] @name"
[600] sys.unix.hw.net.niff.down
[300] sys.unix.hw.net.niff.up
[200] sys.unix.hw.net.niff.alert
```

For additional information regarding NIFF, see the Tru64 UNIX Network Administration Guide for version 5.0A and version 5.1, or the Tru64 UNIX Network Administration: Connections Guide for version V5.1A. You might also check out the niff(7), niffmt(7), niffd(8), and niffconfig(8) reference pages.

# 9.2 Redundant Array of Independent Network Interfaces (NetRAIN)

Tru64 UNIX provides a method of taking multiple network interface cards (NICs) and grouping them together to function as one highly available network, more commonly known as a redundant array of independent network adapters or NetRAIN.

NetRAIN is a virtual interface that works by grouping two or more NICs into an array seen by the operating system as one interface. Each NetRAIN interface uses only one IP address, and there is only one active NIC at any time (for multiple active NICs with one IP address, see "Link Aggregation" in the following section). If the active NIC fails, an idle NIC comes online. The coolness factor in this is that if you happen to be connected to the system via the NetRAIN interface