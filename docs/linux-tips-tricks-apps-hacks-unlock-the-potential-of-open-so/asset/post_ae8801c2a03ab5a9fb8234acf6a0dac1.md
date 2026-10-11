
# Build network clients, servers and more with Netcat

> Learn how to use Netcat to accomplish tasks like creating a web server and a chat server

- Resources
- Linux machine with Netcat
- Root privileges

**Netcat is a simple but handy UNIX utility that reads and writes data across network connections, using either TCP or UDP.** Although it is called Netcat, you can also run it as nc - usually, both commands point to the same binary file.

Most of the command line options of Netcat don't need root privileges to operate. Nonetheless, depending on the port number that you want to use when creating a TCP/IP server, you may need administrative privileges to run Netcat because port numbers 0-1024 are restricted, and can only be used by the root user. As a general principle, it is better to avoid these port numbers and choose something else, provided that it is not already in use by another process.

Is Netcat a panacea? Of course not! No single tool can solve every problem. Is Netcat useful? Yes, and that's the main reason that you should learn how to use it.

## 01 Install Netcat

You can easily install Netcat on a Debian system with the following command:

```bash
# apt-get install netcat-traditional
```

You can also install Netcat using the netcat-opensbd package. The OpenBSD version supports IPv6, proxies and Unix sockets, which are missing from the traditional implementation. In practice, if you don't need these features you won't notice any difference between the two packages.

**Below** You can use the tcpdump utility to capture network traffic to or from particular ports

![](img/30dc0459712b32ede1a3814d456b41b6_45_0.png)

## 02 Basic Netcat usage

The general form of a Netcat command looks like the following:

```text
$ netcat [options] host port
```

The default Netcat behaviour is similar to a simulated network interaction that uses the `telnet` command, which means that the network connection is not secure (ie unencrypted) and that the default protocol is TCP.
If you want, you can also specify a range of ports using the minus character between the two port numbers that indicate the range.

> “Default Netcat behaviour is similar to a simulated network interaction”

## 03 Netcat as a client

The most common Netcat usage is acting as a client for a server process. This is mostly used for troubleshooting network servers because you can see the raw data of the full interaction. The following command will interact with an SMTP server:

```text
$ nc linode 25
```

As you can guess, you can give either the host name or the IP address of the remote host.

## 04 Use files for input and output

According to Unix philosophy, the input to a program can be read from a file and the output can be captured into a file. The input is defined as `filename` and the output as `filename`. You can also use Unix pipes to get your input from the output of other processes.

![](img/30dc0459712b32ede1a3814d456b41b6_46_0.png)

## 05 Netcat as a server

Not only you can use Netcat as a client, you can also use it for creating a server! The next command makes Netcat listen to port number 1234 for incoming TCP connections:

```text
$ netcat -l 1234
```

The job is done by the `-l` option because it tells Netcat to listen for incoming connections. The port number is also provided in the command line.

![](img/30dc0459712b32ede1a3814d456b41b6_46_1.png)

## 06 The UDP protocol

By default, all Netcat interactions work with the TCP protocol. However, it’s also possible to use the UDP protocol if is specified with the use of the `-u` option. This is particularly valuable because Telnet can only test TCP services. The following command tries to test a DNS server that uses UDP:

```text
$ netcat -vv -u 8.8.8.8 53
```

You can create a UDP server if you combine the `-l` option with the `-u` option.

![](img/30dc0459712b32ede1a3814d456b41b6_46_2.png)

## 07 Use Netcat for port scanning

Netcat can be used for port scanning as a naive version of Nmap. The next command scans the 192.168.2.1 IP address using a range of port numbers from 20 to 40:

```text
$ netcat -z -v -n 192.168.2.1 20-40
```

The `-z` option tells Netcat to send zero data. In other words, Netcat closes the connection as soon as it opens it, without any actual data exchange taking place. The `-n` option tells Netcat to disable DNS lookup for the given IP address.

> **Above** You can see details on the Netcat package right at the top of this output
>
> **Finding the problem**
>
> As you already know, there are many tools that can be used for network troubleshooting, including netstat, top, ifconfig, ping, traceroute, netcat, telnet, etc. If you cannot find and solve the problem you are experiencing using this software, you should always have in mind that an erroneous network device can sometimes cause strange networking problems, so you might need to start looking at your hardware instead.

## 08 File transfer

Netcat can also do things that other similar utilities can't do at all. One of those rare things is file transferring. First, you should start the server part as follows:

```bash
$ cat fileToTransfer | nc -l 4567
```

Next, get the file using the subsequent Netcat command:

```bash
$ nc localhost 4567 > fileToTransfer
```

As you can see, you should choose the file that you want to transfer in advance.

> "Firewalls and routers can make Netcat misbehave when used for creating a server"

## 09 Make any process a server

Netcat enables you to make any process a server with the -e parameter. Let's now make /bin/bash a server process; the server part should start as follows:

```bash
$ nc.traditional -vv -l -p 12345 -e /bin/bash
```

The client part should start as follows:

```bash
$ nc -vv <remote_host> 12345
```

![](img/30dc0459712b32ede1a3814d456b41b6_47_0.png)

After the last command, you can start executing commands as if you were working on the remote machine. Note that this capability of Netcat can introduce security threats when used improperly, so be very careful with it.

## 10 Use Netcat as a simple web server

Let's say that you want to serve a simple HTML page from your machine that has the 192.168.2.4 IP address, but you are not able to run a web server. This part will show how to serve it using Netcat without the need for a web server. First, you will need to create a simple HTML file called index.html. Then you will need to start a Netcat server as follows:

```bash
$ netcat -l 4567
```

If you visit http://192.168.2.4:4567/ using your web browser, you will see index.html.

## Picking your tools

Knowing more than one tool is always useful when a new tool is misbehaving. The Ubuntu core team recommends this command and its version number. Their documentation shows that they are not easy to use, and it sometimes makes you look for the right tool. A recent flaw is in ncat's code. The best practice is to try the specific tool that can do your job. But before moving on to Windows tools, we'll check out the top commands.

## 11 Verbose output

Netcat can generate richer output to help you when troubleshooting. You should use the -v command line parameter to make Netcat give more verbose output. Using -vv instead of just -v gives a larger amount of verbose output, which is very useful.

![](img/30dc0459712b32ede1a3814d456b41b6_47_1.png)

## 12 Troubleshoot a web server

The HTTP service is just a TCP service, so Netcat can be used to get data from a web server. This command initiates a connection to a web server:

```bash
$ netcat www.linuxuser.co.uk 80
```

In order to get some output, you should first type in GET / HTTP/1.1 and then press Enter two or three times to start seeing the information. Alternatively, you can always use the following single-line method, which doesn't require any additional typing from you:

```bash
$ echo -en "GET / HTTP/1.0\r\n\r\n" | netcat www.linuxuser.co.uk 80
```

![](img/30dc0459712b32ede1a3814d456b41b6_47_2.png)

## 13 Create a chat server with Netcat

You can get two users from the same or different machines talking to each other by creating a chat server. You should start the server part as follows:

```bash
$ netcat -l 1234
```

Each client that wants to connect to the server must execute the following command:

```bash
$ netcat -vv localhost 1234
```

Only two machines can participate at the same time: the server and only one client. If a second client tries to connect while another one is already connected, the following error message will appear to the second client:

```text
netcat: connect to localhost port 1234 (tcp) failed: Connection refused
```
