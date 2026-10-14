On our two-member cluster, we have a tape device on a shared bus. As we stated in section 15.1.2.2, a tape device is not a DAIO device. Before showing how the I/O flows through the DRD for our served tape device, let’s see which member is currently serving it.

```
[sheridan]
# drdmgr tape0

    View of Data from member sheridan as of 2001-07-24:14:34:56
        Device Name: tape0
        Device Type: Served Tape
        Device Status: OK
        Number of Servers: 2
        Server Name: sheridan
        Server State: Not Server
        Server Name: molari
        Server State: Server
        Access Member Name: molari
        Open Partition Mask: 0
        Statistics for Client Member: sheridan
        Number of Read Operations: 0
        Number of Write Operations: 0
        Number of Bytes Read: 0
        Number of Bytes Written: 0
        Statistics for Client Member: molari
        Number of Read Operations: 0
        Number of Write Operations: 0
        Number of Bytes Read: 0
        Number of Bytes Written: 0
```

```
[sheridan]
# drdmgr -h molari tape0

    View of Data from member molari as of 2001-07-24:14:35:24
        Device Name: tape0
        Device Type: Served Tape
        Device Status: OK
        Number of Servers: 2
        Server Name: sheridan
        Server State: Not Server
        Server Name: molari
        Server State: Server
        Access Member Name: molari
        Open Partition Mask: 0
        Statistics for Client Member: sheridan
        Number of Read Operations: 0
        Number of Write Operations: 0
        Number of Bytes Read: 0
        Number of Bytes Written: 0
```

As we can see from the output above, molari is the server. Since the statistics on the device are currently zero for both members, we will not need to reset the statistics before starting our example. If you’re playing along with the home version (i.e., you are doing these examples on your cluster), however, your device might have counters greater than zero, so you may want to reset them before continuing. Okay, let’s do some I/O.