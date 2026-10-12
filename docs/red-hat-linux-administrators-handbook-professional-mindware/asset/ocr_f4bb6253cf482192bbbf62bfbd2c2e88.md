```
UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
    RX packets:9470  errors:0  dropped:0  overruns:0  frame:0
    TX packets:7578  errors:0  dropped:0  overruns:0  carrier:0
    collisions:0
Interrupt:5  Base address:0x340
```

Here, *ifconfig* reports that network interface device *eth0* has Internet address (*inet addr*) 206.171.50.50, broadcast address (*Bcast*) 206.171.50.63, and network mask 255.255.255.240. The rest of the information shows how many packets this *interface* has received so far (*RX packets*), how many packets this *interface* has transmitted so far (*RX packets*), how many errors of different types have occurred so far, what *interrupt* address line is being used for this device, what *I/O address base* is being used, and so on.

You can run *ifconfig* without any arguments to get the full list of all the up network devices. Note that the *ifup* script uses *ifconfig* to bring up an interface. For example,

```
ifconfig eth0  206.171.50.50 netmask 255.255.255.240 \
    broadcast 206.171.50.63
```

*starts* *eth0* with IP address 206.171.50.50. You can also quickly take down an interface by using the *ifconfig* command. For example, the following command takes down the *eth0* interface:

```
ifconfig eth0 down
```

After the *interface* is up and running, try to contact a computer in your network. You can use the *ping* *IP address* command to see whether your new *interface* can be used to contact a host on the same network.

If your */etc/resolv.conf* file was not set up properly during installation, you will not be able to ping a host using its *host name*. The */etc/resolv.conf* file looks like the following:

```
search nitec.com
nameserver 206.171.50.50
```

This is set up during Red Hat Linux installation. If you have specified an invalid IP address for the name server, your computer will not be able to contact the name server. So, if your network interface is up but you are