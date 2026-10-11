![](bbox=[0.13, 0.03, 0.29, 0.07])

Server: Apache/2.2.20 (Ubuntu)
**Location: http://admin.megacorphone.com:81/admin/**
Vary: Accept-Encoding
Content-Length: 333
Content-Type: text/html; charset=iso-8859-1

```html
<!DOCTYPE HTML PUBLIC "-//IETF//DTD HTML 2.0//EN">
<html><head>
<title>301 Moved Permanently</title>
</head><body>
<h1>Moved Permanently</h1>
<p>The document has moved <a href="http://admin.megacorphone.com:81/admin/">here</a>.
</p>
<hr>
<address>Apache/2.2.20 (Ubuntu) Server at admin.megacorphone.com Port 81</address>
</body></html>
```

*Listing 133 - Using tcpdump with some advanced filtering*

From here, our story becomes clearer. We see a significant amount of failed attempts to authenticate to the **admin** directory, which resulted in HTTP 401 replies, while the last attempt to login seems to have succeeded, as the server replied with a HTTP 301 response. It seems someone gained access to one of megacorphone’s servers!

# 4.5.3.1 Exercises

+   1.  Use **tcpdump** to recreate the Wireshark exercise of capturing traffic on port 110.
+   2.  Use the `-X` flag to view the content of the packet. If data is truncated, investigate how the `-s` flag might help.
+   3.  Find all ‘SYN’, ‘ACK’, and ‘RST’ packets in the `password_cracking_filtered.pcap` file.
+   4.  An alternative syntax is available in tcpdump where you can use a more user-friendly filter to display only ACK and PSH packets. Explore this syntax in the tcpdump manual by searching for “tcpflags”. Come up with an equivalent display filter using this syntax to filter ACK and PSH packets.

# 4.6 Wrapping Up

In this module, we demonstrated some practical tools that are found in every pentester’s toolkit including *Netcat, Socat, PowerShel, Wireshark*, and *Tcpdump*. These tools can assist in many ways during a penetration test, especially when a target is lacking in specialized tools or when we need to transfer small tools to expand our foothold on the target network.