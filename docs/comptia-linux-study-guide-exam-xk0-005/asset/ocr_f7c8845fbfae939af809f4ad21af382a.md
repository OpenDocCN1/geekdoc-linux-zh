# # Examining Sockets

The netstat tool provides a wealth of network information, but it can often be hard to determine just which program is listening on which open port. The `ss` command can come to your rescue for that.

A program connection to a port is called a *socket*. The `ss` command can link which system processes are using which network sockets that are active:

```
$ `ss` -anpt

State Recv-Q Send-Q Local Address:Port Peer Address:Port
LISTEN 0 100 127.0.0.1:25 *:*
LISTEN 0 128 \*111 \*:\*
LISTEN 0 5 192.168.122.1:53 \*:\*
LISTEN 0 128 \*222 \*:\*
LISTEN 0 128 127.0.0.1:631 \*:\*
LISTEN 0 100 ::1:25 ::\*\*
LISTEN 0 128 ::111 ::\*\*
LISTEN 0 128 ::122 ::\*\*
LISTEN 0 128 ::1:631 ::\*\*
ESTAB 0 0 ::1:22 ::1:40490
ESTAB 0 0 ::1:40490 ::1:22
users:(\"ssh",pid=15176,fd=3))
```

The -anpt option displays both listening and established TCP connections and the process they’re associated with. This output shows that the ssh host (port 22) has an established connection and is controlled by process ID 15176, the ssh program.

# ## Monitoring the Network

Often when troubleshooting network applications it helps to see what’s going on “behind the scenes” in the network. Knowing what TCP or UDP packets are being sent between the client and server can be crucial in determining what’s going wrong. Fortunately, Linux has a few different tools that can help with that:

+   * `tcpdump`—the legacy command-line tool for watching network packets
+   * `wireshark`—a graphical tool for watching network packets and performing advanced network analysis
+   * `tshark`—the command-line version of Wireshark

The `tcpdump` program is a legacy tool that’s been around for a long time, but it can still be useful if that’s all you have to work with. It provides simple capturing of network data on the system and can do rudimentary decoding of the packets to break out the different data contained within the network packet.