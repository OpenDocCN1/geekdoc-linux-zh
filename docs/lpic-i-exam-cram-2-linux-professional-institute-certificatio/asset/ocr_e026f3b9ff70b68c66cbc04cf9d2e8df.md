```
11 165.117.200.66 63.039 ms 62.622 ms 62.201 ms
12 165.117.192.38 61.137 ms 53.314 ms 115.764 ms
13 165.117.200.45 82.695 ms 93.937 ms 94.976 ms
14 165.117.192.18 93.599 ms 97.354 ms 93.501 ms
15 165.117.200.1 102.788 ms 116.023 ms 110.338 ms
16 165.117.192.2 91.001 ms 116.288 ms 123.706 ms
17 165.117.200.6 127.074 ms 188.897 ms 110.655 ms
18 165.117.175.133 111.660 ms 133.583 ms 129.227 ms
19 165.117.48.182 132.952 ms 110.658 ms 175.021 ms
20 165.117.178.84 130.887 ms 99.306 ms 135.562 ms
21 67.95.172.210 120.904 ms 132.106 ms 203.681 ms
22 207.238.213.12 150.149 ms 132.494 ms 111.996 ms
```

If you see a series of (* asterisks) where a return time should be, that’s an indication that the router is either configured to not return **ECHO_REQUESTS** from traceroute or it’s too busy or even down and can’t respond. That is typically the bottleneck or problem that caused you to start troubleshooting in the first place.

When you’re troubleshooting a user’s access problem, it can be a number of things, the most likely of which are

+   - **User can’t connect to anything**\—This is a local IP or network mask problem. If she can’t even ping someone on her local network, her machine is the problem.
+   - **User can see her network, but not others**\—This is a problem with her default gateway. The only path out of her network is misconfigured.
+   - **User can see internal network, but not Internet**\—This is usually a firewall or even DNS problem. If she can ping Internet sites by IP, but not name, it’s definitely DNS.

For all these instances, use **ping** first. Then, if you can’t find the problem or it’s outside your area of responsibility, use **traceroute**.

# ### Using tcpdump

The **tcpdump** utility is used to capture and display packets from a network. Either you can search the output in real time by redirecting the captured data to **grep** or the data can be written to a file for later searching.

**tcpdump** has a dizzying array of options to choose from; the **man** page for most versions rivals the **bash** man page. A couple of half-hour sessions with a few machines and the **tcpdump** man page will have you past the dangerous stage and able to use **tcpdump** properly for troubleshooting and security assessments.

To use **tcpdump** to capture all the data going across your local network and put that data in a file, you would use the command shown here:

```
tcpdump -w capturefile.cap
```