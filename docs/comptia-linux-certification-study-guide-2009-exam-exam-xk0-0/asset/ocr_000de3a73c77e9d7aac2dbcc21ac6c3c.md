```
doing it by hand — so I use the alias command to create a whole new command,
pdg for “ping default gateway.”
chappel@agatha:~$ pdg
PING 192.168.10.1 (192.168.10.1) 56(84) bytes of data.
64 bytes from 192.168.10.1: icmp_seq=1 ttl=64 time=0.686 ms
64 bytes from 192.168.10.1: icmp_seq=2 ttl=64 time=0.484 ms
64 bytes from 192.168.10.1: icmp_seq=3 ttl=64 time=0.484 ms
--- 192.168.10.1 ping statistics ---
3 packets transmitted, 3 received, 0% packet loss, time 1998 ms
rtt min/avg/max/mdev = 0.484/0.551/0.686/0.097 ms
chappel@agatha:~$
```

# Special Devices

You may have noticed some particularly unusual files when peeking into the `/dev` subdirectory:

+   - /dev/null
+   - /dev/random
+   - /dev/zero
+   - /dev/urandom

The /dev/null file is often called the *bit bucket*, and is like having your own personal black hole. Any output you don’t need to see? Ever? Just redirect it to the bit bucket. This is most often used to hide unnecessary output from a program embedded in a script.

The /dev/random file does just what it says: it’s the interface to the systems random number generator and will produce random numbers used to create very secure cryptographic keys. Creating true random numbers is difficult for a computer, though. Current Linux systems use noise from various device drivers and other nonrepeating information to maintain an “entropy