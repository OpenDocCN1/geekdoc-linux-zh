# # ping

The ping (Packet Internet Groper) program is used to query another system and ensure a connection is active. The ping program operates by sending a request to the destination machine for a reply. If the destination machine's IP software receives the request, it issues a reply immediately.

The sending machine continues to send requests until the ping program is terminated with a break sequence. After termination, ping displays a set of statistics. A sample ping session is shown as follows:

```
prudie> ping merlin
PING merlin: 64 data bytes
64 bytes from 142.12.130.12: icmp_seq=0. time=20. ms
64 bytes from 142.12.130.12: icmp_seq=1. time=10. ms
64 bytes from 142.12.130.12: icmp_seq=2. time=10. ms
64 bytes from 142.12.130.12: icmp_seq=3. time=20. ms
64 bytes from 142.12.130.12: icmp_seq=4. time=10. ms
64 bytes from 142.12.130.12: icmp_seq=5. time=10. ms
64 bytes from 142.12.130.12: icmp_seq=6. time=10. ms
--- merlin PING Statistics ---
7 packets transmitted, 7 packets received, 0% packet loss
round-trip - min/avg/max = 10/12/20
```

If ping was unable to reach the remote machine, it displays error messages. You can also ping the localhost, which shows if there is an error in the loopback driver configuration files.

The ping program is useful because it provides four important pieces of information: whether the TCP/IP software is functioning correctly, whether a local network device can be addressed (validating its address), whether a remote machine can be accessed (again validating the address and testing the routing), and verifying the software on the remote machine.

# # Summary

In this chapter, you've seen how to install, configure, and test Ethernet connections to your Linux machine. The next chapter looks at the SLIP and PPP protocols used by many Linux boxes to connect to an ISP. The only other networking process usually found on a Linux box uses UUCP (UNIX-to-UNIX Copy), which is described in Chapter 44, “NIS and YP.”

If you want to install a network to connect several of your machines (assuming you have more than one), you will find it quite easy and useful. If you have two machines, it is fast and efficient to connect a Linux machine and a DOS or Windows machine, as long as the other machine is running TCP/IP. There are shareware versions of TCP/IP for Windows and many commercial implementations for both DOS and Windows.