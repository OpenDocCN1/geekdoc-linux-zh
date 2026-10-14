```
initdead 30
keepalive 2
logfacility local0
node node1.example.org
node node2.example.org
respawn hacluster /usr/lib/heartbeat/ipfail
ping 172.16.245.5 172.16.245.1
auto_failback off
```

A copy of this file will go on both node1 and node2. Each of these options is important, so I describe them here:

+   - **autojoin**  
+     You can choose to have nodes automatically join a cluster using the shared secret in the authkey file as authentication. For large clusters that constantly add or delete nodes this might be a useful option to enable so that you aren’t constantly rolling out and updating your ha.cf file to list new nodes. In my case, since I have only two nodes, I have disabled this option.
+   
+   - **bcast**  
+     There are a number of different ways each node can communicate to the others for Heartbeat and other communications. Each of these options is documented in /usr/share/doc/heartbeat/ha.cf.gz, but here is a summary. If you use the serial option, you can check Heartbeat over a null modem cable connected to each node’s serial port. If you use mcast, you can define a multicast interface and IP address to use. In my case I used bcast, which broadcasts over my eth1 interface (the private network I set up). You can also specify ucast, which allows you to simply communicate via a unicast IP. That could be useful if you want to limit broadcast traffic or if you have only one interface (or a pair of bonded ports) and want to use standard IP addresses to communicate. By default Heartbeat uses UDP port 694 for communication, so if you have a firewall enabled, be sure to add a rule to allow that access.
+   
+   - **warntime**  
+     This is the time in seconds during which a communication can time out before Heartbeat will add a note in the logs that a node has a delayed heartbeat. No action will be taken yet.