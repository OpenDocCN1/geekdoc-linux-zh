Press Ctrl+C to end the `ping` command. The lines above show the responses from www.hansonhistory.com. It sent back packets from the IP address 198.60.22.8 in response to each one I received. You can see the sequence of packets (icmp\_seq) and the time it took for each response (in milliseconds). If you receive packets in return, you will know two things: first, that your connection is working, and second, that your name to address translation (from the DNS addresses in `/etc/resolv.conf`) is working.

# Checking the default route

After starting a dial-up connection, check that the default route is set using `route -n`.

```
# /sbin/route -n
Kernel IP routing table
Destination    Gateway     Genmask         Flags Metric Ref  Use Iface
198.62.1.1     0.0.0.0     255.255.255.255 UH    0      0    0 ppp0
10.0.0.0       0.0.0.0     255.0.0.0       U     0      0    0 eth0
127.0.0.0      0.0.0.0     255.0.0.0       U     0      0    0 lo
0.0.0.0        198.62.1.1  0.0.0.0         UG    0      0    0 ppp0
```

This shows that the gateway was set to the remote PPP server (198.62.1.1), as well as showing the other interfaces running on my computer. There are two ppp0 entries. The first shows the destination as a host (UH). The second shows the destination as a gateway (UG). All addresses that can’t be resolved on the local LAN are directed to the gateway address.

# Checking that the name servers are set

If you are able to ping a remote computer by IP address, but are not able to resolve any addresses, your DNS servers may not be set correctly. As root user from a Terminal window, open the `/etc/resolv.conf` file and check that there are lines identifying one or more DNS servers in this file. These should be supplied to you by your ISP (unless you run your own DNS server). Here are some examples (the numbers are fictitious):

```
nameserver    111.111.111.111
nameserver    222.222.222.222
```

Try using the `ping` command to make sure that the name servers are live.

# Checking the chap-secrets or pap-secrets file

PPP supports two authentication protocols in Red Hat Linux: Challenge Handshake Authentication Protocol (CHAP) and Password Authentication Protocol (PAP). Here is what each protocol does to authenticate:

+   CHAP — The server sends the client a challenge packet (which includes the server name). The client sends back a response that includes its name and a value that combines the secret and the challenge. The client name and secret are stored in your `/etc/ppp/chap-secrets` file.