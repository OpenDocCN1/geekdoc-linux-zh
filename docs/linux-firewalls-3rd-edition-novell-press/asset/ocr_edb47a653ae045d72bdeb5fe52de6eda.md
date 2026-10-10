```
tcpdump 'port 80 and (host 192.168.1.10 or host 192.168.1.11)'
```

Parentheses are required only for logical grouping. In practice, you’ll suffer no penalty for using them, and truthfully I normally use them just out of habit. When writing the preceding simple **port 80** example, I included the parentheses at first only to go back and remove them after I thought about what I was doing. Old habits die hard. Speaking of unnecessary terms, the term **host** in the example isn’t required either—more on that later.

Here are some examples using the net type qualifier to listen for traffic:

```
tcpdump 'net 192.168.1' 
```

Here’s that same example using CIDR notation:

```
tcpdump 'net 192.168.1.0/24' 
```

And finally, here’s that same example using the mask modifier:

```
tcpdump 'net 192.168.1.0 mask 255.255.255.0' 
```

If you fail to specify a type qualifier (host, net, port) within a TCPDump expression, the host type is assumed. Therefore, don’t be surprised when you receive a “parse error” when attempting something like this:

```
tcpdump '80' 
```

Really, you probably wanted to have TCPDump listen for traffic on port 80:

```
tcpdump 'port 80' 
```

# TCPDUMP'S DIRECTION QUALIFIER

Another kind of qualifier within a TCPDump expression is the direction qualifier. The previous examples will look for traffic flowing in either direction, coming or going, on port **80** for instance. For example, this might mean that traffic destined for a web server running at **192.168.1.10** will be captured but so will traffic leaving the computer at **192.168.1.10** and destined for another server on port **80**. You can also specify the direction with which to capture traffic by using a direction qualifier. The terms **src** for the source and **dst** for the destination are the two direction qualifiers used by TCPDump. Adding the destination term to one of the previous examples yields an expression that will look for port 80 traffic going to **192.168.1.10** or **192.168.1.11**:

```
tcpdump 'port 80 and (src 192.168.1.10 or src 192.168.1.11)' 
```

The direction qualifier isn’t limited to looking for traffic on certain addresses. It’s perfectly valid to look for traffic with a source or destination of a specific port, as in this example that looks for traffic with a destination of port 25 (usually SMTP):