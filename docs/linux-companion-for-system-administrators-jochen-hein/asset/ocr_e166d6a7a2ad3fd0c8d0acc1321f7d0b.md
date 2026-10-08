# 392 LINUX IN A NETWORKED ENVIRONMENT

The first command looks after transport of packets from its own computer to the SLIP server, which is called sliprv. In the second step, a route to the subnet 192.168.66.0 is entered which is transferred via the SLIP server. For this purpose, it must be configured as gateway (IP forwarder). If you are not connected to a local network and connect to your provider (and thus the Internet) via SLIP or PPP, you must specify a default route.

A route can be deleted from the routing table, for example in case of problems or termination of a dial-in connection, by means of the parameter del. The following command removes the routing entries of the SLIP connection used in the previous example.

```
route del -net 192.168.66.0
route del sliprv
```

# 13.6 The netstat program

The netstat program is another alternative for obtaining information on the current state of the network. It provides a number of options which display different kinds of information. netstat combines a series of utilities in one program. The different functions are selected via options.

+   - -a generates a list of all Internet sockets, that are TCP, UDP, RAW, and UNIX sockets, including the ports that are only listening. This command informs you about the existing connections and their status, as well as your system provides to the net.

+   - -i displays statistics on the network devices. All sent and received packets are shown, together with the errors, drops, and overruns that occurred. A sample output can be found in Listing 13.6. In the last column, you will find a series of flags which describe the configuration of the interfaces in more detail. These flags are listed in Table 13.4.

```
(Linux):# netstat -i
kernel Interface table
Iface MT MT-RX RX-ERR RX-DRP RX-OVR TX-OK TX-ERR TX-DRP TX-OVR Flags
lo 2000 0 0 0 0 89 0 0 0 BLU
tr0 2000 0 10840 0 0 1000 0 0 BRU
```

Listing 13.6 Output of the netstat -i command.