This captures packets on port 80.

4. **Capture packets from a specific IP and port:**

```
tcpdump src 192.168.1.2 and port 22
```

This captures packets where the source IP is 192.168.1.2 and the port is 22.

5. **Capture and display packet details in verbose mode:**

```
tcpdump -v
```

This command provides more detailed information about each captured packet.

6. **Capture a specific number of packets:**

```
tcpdump -c 10
```

This captures and displays the first 10 packets, then exits.

7. **Write captured packets to a file:**

```
tcpdump -w capture.pcap
```