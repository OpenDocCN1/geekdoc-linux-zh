# **98. tcpdump: Capture and display network traffic.**

`tcpdump` is a powerful command-line packet analyzer tool that allows you to capture and display network traffic on a Linux system. It is widely used for network troubleshooting, analysis, and security auditing.

**Examples:**

+   1. **Capture all packets on a specific interface:**

```
```
tcpdump -i eth0
```
```

This command captures all packets on the `eth0` interface.

+   2. **Capture packets with a specific source or destination IP address:**

```
```
tcpdump host 192.168.1.2
```
```

This captures packets where the IP address 192.168.1.2 is either the source or destination.

+   3. **Capture packets on a specific port:**

```
```
tcpdump port 80
```
```