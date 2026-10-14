```
Feb 16 17:37:59 node2 ipfail: [4340]: debug: Message [you_are_dead] sent.
Feb 16 17:38:05 node2 heartbeat: [4255]: info: node1 wants to go standby [all]
Feb 16 17:38:06 node2 ipfail: [4340]: debug: Other side is unstable.
Feb 16 17:38:06 node2 heartbeat: [4255]: info: standby: acquire [all] resources from node1
Feb 16 17:38:06 node2 heartbeat: [4443]: info: acquire all HA resources (standby).
Feb 16 17:38:06 node2 ResourceManager[4457]: info: Acquiring resource group: node1 172.16.245.222 apache2
Feb 16 17:38:06 node2 IPaddr[4483]: INFO: Resource is stopped
Feb 16 17:38:06 node2 ResourceManager[4457]: info: Running /etc/ha.d/resource.d/IPaddr 172.16.245.222 start
Feb 16 17:38:06 node2 ResourceManager[4457]: debug: Starting /etc/ha.d/resource.d/IPaddr 172.16.245.222 start
Feb 16 17:38:07 node2 IPaddr[4554]: INFO: Using calculated nic for 172.16.245.222: eth0
Feb 16 17:38:07 node2 IPaddr[4554]: INFO: Using calculated netmask for 172.16.245.222: 255.255.255.0
Feb 16 17:38:07 node2 IPaddr[4554]: DEBUG: Using calculated broadcast for 172.16.245.222: 172.16.245.255
Feb 16 17:38:07 node2 IPaddr[4554]: INFO: eval ifconfig eth0:0 172.16.245.222 netmask 255.255.255.0 broadcast 172.16.245.255
Feb 16 17:38:07 node2 IPaddr[4554]: DEBUG: Sending gratuitous Arp for 172.16.245.222 on eth0: [eth0]
Feb 16 17:38:07 node2 kernel: [ 7391.316832] NET: Registered protocol family 17
Feb 16 17:38:07 node2 IPaddr[4539]: INFO: Success
Feb 16 17:38:07 node2 ResourceManager[4457]: debug: /etc/ha.d/resource.d/IPaddr 172.16.245.222 start done. RC=0
Feb 16 17:38:07 node2 ResourceManager[4457]: info: Running /etc/init.d/apache2 start
Feb 16 17:38:07 node2 ResourceManager[4457]: debug: Starting /etc/init.d/apache2 start
Feb 16 17:38:07 node2 ResourceManager[4457]: debug: /etc/init.d/apache2 start done. RC=0
Feb 16 17:38:07 node2 heartbeat: [4443]: info: all HA resource acquisition completed (standby).
Feb 16 17:38:08 node2 heartbeat: [4255]: info: Standby resource acquisition done [all].
Feb 16 17:38:08 node2 heartbeat: [4255]: info: remote resource transition completed.
Feb 16 17:38:08 node2 ipfail: [4340]: debug: Other side is now stable.
Feb 16 17:38:08 node2 ipfail: [4340]: debug: Other side is now stable.
```

Now you can plug the interface back in. If you disabled automatic fail-over, the other node will still hold the floating IP. Otherwise the cluster will