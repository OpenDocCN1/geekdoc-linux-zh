
![](img/c0a399aca0d18f8822d714ad0a173123_279_0.png)

If you have multiple network interface cards on your Linux system and choose to connect them to separate networks, you can configure your Linux system to act as a bridge between the two networks. The `brctl` command allows you to control how the bridging behaves. To do this, though, you must set the `ip_forward` kernel parameter in the `/etc/sysctl.conf` file to 1 to enable bridging.

## Command-Line Networking Tool

Linux provides a wealth of networking tools for connecting to remote hosts, but none is more versatile than the *netcat* program. The *netcat* program can act as either a network server or network client, sending and receiving data packets using either TCP or UDP. This section provides some examples of the versatility of the *netcat* program.

Depending on your Linux distribution, the *netcat* program may be available as either *netcat*, or just *nc*. The format of the command is simply:

```
nc host port
```

where *host* is the IP address or hostname of the remote server and *port* is the port number for the connection. By default *netcat* will attempt to establish a TCP connection with the remote server. To establish a UDP connection, add the `-u` option.

There are lots of different options available to customize the connection. Table 7.4 lists the *netcat* options.

**TABLE 7.4** The *netcat* command options

| Option | Description |
| :--- | :--- |
| `-4` | Use only IPv4 addresses |
| `-6` | Use only IPv6 addresses |
| `-c` | Use a carriage return/linefeed combination at the end of each line |
| `-D` | Enable socket debugging |
| `-d` | Do not read from STDIN |
| `-h` | Displays the *netcat* help document |
| `-i` | Specify a delay interval between text sent and received |
| `-k` | Continuing listing for an incoming connection after the current connection terminates |
| `-l` | Listing for an incoming connection instead of initializing a new connection |
| `-n` | Do not use DNS lookups for hostnames |
| `-p` | Specifies the port used for the connection |
| `-r` | Use a random source and/or destination port |
| `-S` | Enables the MD5 signature option |
| `-s` | Specify the IP address of the network interface used for sending packets |
| `-T` | Specify the IP Type of Service (ToS) used for the connection |
| `-t` | Reply to Telnet protocol options send from servers |
| `-U` | Uses Unix domain sockets instead of network sockets |
| `-u` | Use UDP instead of TCP |
| `-v` | Enable verbose mode to display more information |
| `-w` | Specify a timeout value for inactivity disconnections |
| `-X` | Use SOCK or HTTP proxy server protocols |
| `-x` | Specify the proxy server to use for the connection |
| `-z` | Scan for listening applications rather than attempting to connect |

A great troubleshooting feature of nc is the ability to send HTTP requests directly to servers and see the HTTP response as well as the HTML code returned. Listing 7.8 shows an example of the output you would see.

### Listing 7.8: Using netcat to retrieve HTTP data

```
$ printf "GET / HTTP/1.0\r\n\r\n" | nc richblum.com 80
HTTP/1.1 200 OK
Date: Mon, 04 Dec 2021 16:14:35 GMT
Server: Apache
Vary: Accept-Encoding
Connection: close
Content-Type: text/html
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN"
  "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
<html xmlns="http://www.w3.org/1999/xhtml">
<head>
  <link rel="stylesheet" type="text/css" href="main/mystyle.css" />
  <link rel="stylesheet" media="print" type="text/css"
        href="main/print.css" />
  <title>Rich Blum's Blog</title>
</head>
```

The output in Listing 7.8 shows the HTTP options sent by the server, followed by the HTML code for the web page.

You can also create a simple chat dialogue between two systems from the command-line. On one system, just start nc in listen mode using the -l option:

```
$ nc -l 8000
```

Then on the other system, connect to that port on the remote system:

```
$ nc hostname 8000
```

Now any text you type in one side displays on the other side! To break the connection, just press Ctrl+C on either side of the connection.

Finally, another great use of the netcat program is as a quick way to transfer a file from one system to another. Just redirect the output of the listening host to a file:

```
$ nc -l 8000 > filename.txt
```

Then on the sending host, redirect the file as input to the sending nc command:

```
$ nc hostname 8000 < myfile.txt
```

When the file transfer completes, both sides of the connection will automatically terminate, and the new file will be available on the receiving host. This makes moving files between systems a breeze!

> If you need to test secure SSL connections with a network server, the s_client package allows you to do that. It can utilize certificates to establish connections with secure servers.

## Basic Network Troubleshooting

Once you have a Linux kernel installed, there are a few things you can do to check to make sure things are operating properly. The following sections walk through the commands you should know to monitor the network activity, including watching what processes are listening on the network and what connections are active from your system.

### Sending Test Packets

One way to test network connectivity is to send test packets to known hosts. Linux provides the `ping` and `ping6` commands to do that. The `ping` and `ping6` commands send *Internet Control Message Protocol (ICMP)* packets to remote hosts using either the IP (*ping*) or IPv6 (*ping6*) protocol. ICMP packets work behind the scenes to track connectivity and provide control messages between systems. If the remote host supports ICMP, it will send a reply packet back when it receives a ping packet.

The basic format for the `ping` command is to specify the IP address of the remote host:

```
$ ping 10.0.2.2
PING 10.0.2.2 (10.0.2.2) 56(84) bytes of data.
64 bytes from 10.0.2.2: icmp_seq=1 ttl=63 time=14.6 ms
64 bytes from 10.0.2.2: icmp_seq=2 ttl=63 time=3.82 ms
64 bytes from 10.0.2.2: icmp_seq=3 ttl=63 time=2.05 ms
64 bytes from 10.0.2.2: icmp_seq=4 ttl=63 time=0.088 ms
64 bytes from 10.0.2.2: icmp_seq=5 ttl=63 time=3.54 ms
64 bytes from 10.0.2.2: icmp_seq=6 ttl=63 time=3.97 ms
64 bytes from 10.0.2.2: icmp_seq=7 ttl=63 time=0.040 ms
^C
--- 10.0.2.2 ping statistics ---
7 packets transmitted, 7 received, 0% packet loss, time 6020ms
rtt min/avg/max/mdev = 0.040/4.030/14.696/4.620 ms
$ 
```

The `ping` command continues sending packets until you press Ctrl+C. You can also use the `-c` command-line option to specify a set number of packets to send and then stop.

For the `ping6` command, things get a little more complicated. If you're using an IPv6 link local address, you also need to tell the command which interface to send the packets out on:

```
$ ping6 -c 4 fe80::c418:2ed0:aaed:cbce%enp0s3
PING fe80::c418:2ed0:aaed:cbce%enp0s3(fe80::c418:2ed0:aaed:cbce) 56 data bytes
64 bytes from fe80::c418:2ed0:aead:cbce: icmp_seq=1 ttl=128 time=1.47 ms
64 bytes from fe80::c418:2ed0:aead:cbce: icmp_seq=2 ttl=128 time=0.478 ms
64 bytes from fe80::c418:2ed0:aead:cbce: icmp_seq=3 ttl=128 time=0.777 ms
64 bytes from fe80::c418:2ed0:aead:cbce: icmp_seq=4 ttl=128 time=0.659 ms

--- fe80::c418:2ed0:aead:cbce%enp0s3 ping statistics ---
4 packets transmitted, 4 received, 0% packet loss, time 3003ms
rtt min/avg/max/mdev = 0.478/0.847/1.475/0.378 ms
```

The `%enp0s3` part tells the system to send the ping packets out the enp0s3 network interface for the link local address.

Yet another useful tool is the `traceroute` command. The `traceroute` command uses a feature of ICMP packets that restrict the number of network “hops” they can make. By manipulating that value in the packet, the `traceroute` command allows you to see the network routers used to get the packets from the client to the server.

Finally, the `mtr` program is a package that utilizes data retrieved from `ping` and `traceroute` commands to document network availability and latency in a real-time chart. Figure 7.4 shows the output of the `mtr` command tracing the connectivity to the `linux.org` server.

### FIGURE 7.4 Using `mtr` to monitor network connectivity to a server

![](img/c0a399aca0d18f8822d714ad0a173123_283_0.png)
