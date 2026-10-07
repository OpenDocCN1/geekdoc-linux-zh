# v.4.33

# A Comprehensive Beginner's Guide to Linux as a Digital Forensic Platform

```
root@forensic1:~# ifconfig eth0 192.168.0.1 netmask 255.255.250
```

```
root@forensic1:~# ifconfig eth0
eth0: flags=4096<UP,BROADCAST,MULTICAST> mtu 1500
      inet 192.168.0.1 netmask 255.255.255.0 broadcast 192.168.0.255
      ether 10:bf:4f:79:a1 txqueuelen 1000 (Ethernet)
      RX packets 198523 bytes 300549068 (2.7 GiB)
      errors 0 dropped 0
      TX packets 872940 bytes 62217638 (59.3 MiB)
      errors 0 dropped 0 overruns 0 carrier 0 collisions 0
device interrupt 20 memory 0xffe20000-f7e20000
```

Now the output above shows the interface is "up", and the address is now
192.168.0.1, and the netmask and broadcast address are also set. For now that's all for our
collection workstation as far as simple configuration goes.

On our subject work, we will need to boot it with a suitable boot disk. I carry
 with me, and just any of them will work as long as we have a robust tool.
Once you boot the subject, repeat the steps above to setup a simple network interface,
making sure that the two computers are physically connected via crossover cable, hub, or
other means. The prompt will change to illustrate what we are working on the SUBJECT
computer now, and not our collection system:

```
root@bootdisk:~# ifconfig eth0 192.168.0.2 netmask 255.255.255.0
```

```
root@bootdisk:~# ifconfig eth0
eth0: flags=4163<UP,BROADCAST,RUNNING,MULTICAST> mtu 1500
      inet 192.168.0.2 netmask 255.255.255.0 broadcast 192.168.0.255
      ether 08:00:27:99:d6:30 txqueuelen 1000 (Ethernet)
      RX packets 73 bytes 11716 (11.4 KiB)
      errors 0 dropped 0 overruns 0 frame 0
      TX packets 16 bytes 1392 (1.3 KiB)
      errors 0 dropped 0 overruns 0 carrier 0 collisions 0
```

Note the IP addresses of our systems:

Subject Computer: 192.168.0.2
Collection System: 192.168.0.1

We can then see if we can communicate with our evidence collection system
(192.168.0.1) using the ping command (which we interrupt with ctrl-c):

# 134