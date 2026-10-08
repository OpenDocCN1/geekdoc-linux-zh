# ### 1. The operating system,

2. The actual services running on those ports, and 3. The version of the services (different versions have different vulnerabilities).

The **-A** switch in nmap can help us with those remaining unknowns.

Such as;

```
kali > nmap -sT -A 192.168.0.157
```

This scan also takes longer to complete as it has much more work to do than simply scan for open ports— a very deterministic process. In this scan, nmap will be probing into each open port with specially crafted packets and then, by evaluating the differences in the response, determine the service and its version. It uses a similar less-deterministic process for determining the operating system. As I outlined in Chapter 5

on **p0f** , each operating system TCP/IP stack places slightly different values in header fields. By reading those fields, we can make highly accurate estimate of the underlying target operating system.