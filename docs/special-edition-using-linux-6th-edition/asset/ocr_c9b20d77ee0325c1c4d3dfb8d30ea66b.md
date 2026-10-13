# Listing 22.3  Continued

```
unix  2     [ ACC ]     STREAM     LISTENING     118740 /tmp/.axsc5
unix  2     [ ACC ]     STREAM     LISTENING     78364  /tmp/.axnetipc
unix  3     [   ]         STREAM     CONNECTED     129400 /tmp/.X11-unix/X0
unix  3     [   ]         STREAM     CONNECTED     129399
unix  3     [   ]         STREAM     CONNECTED     118746 /tmp/.X11-unix/X0
unix  3     [   ]         STREAM     CONNECTED     118745
unix  3     [   ]         STREAM     CONNECTED     118588 /tmp/.X11-unix/X0
unix  3     [   ]         STREAM     CONNECTED     118587
unix  3     [   ]         STREAM     CONNECTED     118468 /tmp/.X11-unix/X0
unix  3     [   ]         STREAM     CONNECTED     118467
unix  3     [   ]         STREAM     CONNECTED     118451 /tmp/.X11-unix/X0
unix  3     [   ]         STREAM     CONNECTED     118450
unix  3     [   ]         STREAM     CONNECTED     118443 /tmp/.X11-unix/X0
unix  3     [   ]         STREAM     CONNECTED     118442
unix  3     [   ]         STREAM     CONNECTED     118428 /tmp/.X11-unix/X0
unix  3     [   ]         STREAM     CONNECTED     118427
unix  3     [   ]         STREAM     CONNECTED     116711 /tmp/.X11-unix/X0
unix  3     [   ]         STREAM     CONNECTED     116710
unix  3     [   ]         STREAM     CONNECTED     116706 /tmp/.X11-unix/X0
unix  3     [   ]         STREAM     CONNECTED     116705
unix  5     [   ]         STREAM     CONNECTED     116694 /tmp/.X11-unix/X0
unix  3     [   ]         STREAM     CONNECTED     116684
unix  3     [   ]         STREAM     CONNECTED     100030 /tmp/mysql.sock
unix  3     [   ]         STREAM     CONNECTED     100028
unix  2     [   ]         DGRAM                    16481
unix  2     [   ]         DGRAM                    421
unix  2     [   ]         DGRAM                    397
unix  2     [   ]         DGRAM                    379
unix  2     [   ]         DGRAM                    375
unix  2     [   ]         DGRAM                    354
unix  2     [   ]         DGRAM                    300
unix  2     [   ]         DGRAM                    292
unix  2     [   ]         DGRAM                    286
netstat: no support for 'AF IPX' on this system.
netstat: no support for 'AF AX25' on this system.
netstat: no support for 'AF NETROM' on this system.
```

The netstat output is clearly labeled at the top of each section. The first section shows that it consists of established connections as well as bound servers. The first column shows the protocol, tcp, udp, or raw, the second and third columns show how many bytes are in the send and receive queues. The byte column will normally be 0, but can be 1 if the state is LAST_ACK.

The next two columns show the local address and port, and the foreign address and port. For established TCP connections, you will have two lines, one in each direction. So in Listing 22.3, you have three connections to port 7100 and three from port 7100 (client to server, server to client). Asterisks show listening servers and the port and address to which they are listening. The 0.0.0.0 means all addresses.

The State column shows you the state of the connection and can be any one of the following:

+   - **ESTABLISHED**—An active connection is made.
+   - **SYN_SENT**—A new connection is being initiated with a foreign host.