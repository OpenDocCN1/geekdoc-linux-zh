# tracepath

Purpose: Display TCP/IP routing information on Linux systems.

**Usage syntax:** `tracepath [OPTIONS] [HOST]`

```
$ tracepath -n www.google.com
1: 192.168.1.64    0.207ms pmtu 1500
1: 192.168.1.254   1.482ms
1: 192.168.1.254   1.263ms
2: 99.60.32.2      27.476ms
3: 76.196.172.4    27.227ms
4: 151.164.94.52   27.428ms
5: 69.220.8.57     37.468ms asynn 7
6: no reply
7: no reply
8: no reply
...
```

![](bbox=[0.28, 0.43, 0.88, 0.45])

The **tracepath** command is a replacement for the **traceroute** command on Linux systems. You can use either program on Linux, but many distributions only include **tracepath** by default. The above example demonstrates using **tracepath** to display the route to www.google.com.

> **Tip** The **tracepath6** command is used to trace IP version 6 hosts.

+   **Common usage examples:**
+   `tracepath [HOST]` Trace the path to the specified host
+   `tracepath -n [HOST]` Do not lookup DNS names when tracing