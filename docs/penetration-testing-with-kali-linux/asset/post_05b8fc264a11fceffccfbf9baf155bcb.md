
## OffSec

Penetration Testing with Kali Linux

| port | status | reason |
| :--- | :--- | :--- |
| 22/tcp | closed ssh | conn-refused |
| 23/tcp | closed telnet | conn-refused |
| 25/tcp | closed smtp | conn-refused |
| 53/tcp | closed domain | conn-refused |
| 80/tcp | open http | syn-ack |
| 110/tcp | closed pop3 | conn-refused |
| 111/tcp | closed rbind | conn-refused |
| 135/tcp | open msprpc | syn-ack |
| 139/tcp | closed netbios-sn | conn-refused |
| 143/tcp | closed imap | conn-refused |
| 443/tcp | closed https | conn-refused |
| 445/tcp | closed microsoft-ds | conn-refused |
| 993/tcp | closed imaps | conn-refused |
| 995/tcp | closed pop3 | conn-refused |
| 1723/tcp | closed pptp | conn-refused |
| 3386/tcp | closed mysql | conn-refused |
| 3389/tcp | open ms-wbt-server | syn-ack |
| 5900/tcp | closed vnc | conn-refused |
| 8080/tcp | closed http-proxy | conn-refused |

Read data files from: /usr/bin/share/nmap
map done: 1 IP (1 host used) in 21.30 seconds

Listing 553 - Scanning MULTISERVER results and discover remote SOCKS port with Proxychains.

After a few minutes, we receive our results and discover ports 80, 135, and 3389 are open.

> Scanning is a little slower against this Windows host - likely due to the different Windows firewall responds when a port is closed compared to Linux.

In this section, we use SSH remote port forwarding to open a SOCKS proxy port on our Kali machine by initiating an SSH connection from a remote compromised host. We then used Proxychains to scan a host on the internal network through the SOCKS proxy port.

### 18.3.5 Using sshuttle

In situations where we have direct access to an SSH server, which is behind a more complex internal network, classic dynamic port forwarding might be difficult to manage. sshuttle⁴ is a tool that turns an SSH connection into something similar to a VPN by setting up local routes that force traffic through the SSH tunnel. However, it requires root privileges on the SSH client and Python3 so it's not always the lightest option. In the appropriate scenario, however, it can be very useful.

In our environment, we have SSH access to PGDATABASE0, which we can access through a port forward set up on CONFLUENCE1. Let's run sshuttle through this to observe its capabilities.

First, we set up a port forward in a shell on CONFLUENCE1, listening on port 2222 on the WAN interface and forwarding to port 22 on PGDATABASE0.

⁴(sshuttle, 2022), https://github.com/sshuttle

```
confluence@01:/opt/atlassian/confluence/bin$ socat TCP-LISTEN:2222,fork
TCP:10.4.50.215:22
</$ socat TCP-LISTEN:2222,fork
```

Listing 554 - Forwarding port 2222 on CONFLUENCE0 to port 22 on PGDATABASE0.

Next, we can run sshuttle, specifying the SSH connection to use, as well as the subnets that we want to tunnel through this connection (10.4.50.0/24 and 172.16.50.0/24).

```
kali@kali:$ sshuttle -r database_admin@192.168.50.63:2222 10.4.50.0/24 172.16.50.0/24
[local sudo] Password:
```

```
database_admin@192.168.50.63:~ password:
Connected to server.
Failed to flush caches: dbus-org.frektop.service not found.
Received non-zero return code 1 when flushing DNS.
```

Listing 555 - Running sshuttle from our Kali machine, pointing to port on CONFLUENCE1.

Although we don't run sshuttle, in theory, it should set up the routing on our Kali machine so that any requests we make to subnets will be pushed through the SSH connection. Let's test if this is working by trying to connect to SMB share on SHARES in a new terminal.

```
kali@kali:$ smclient -L //172.16.50.217 -U hr_admin --password=Welcome123
```

| Share Type | Comment |
| :--- | :--- |
| ADMIN | Remote Admin |
| CS | Default share |
| IPC | scripts |

Reconnecting with SMB workgroup:connect to 172.16.50.217 failed (NT_STATUS_RESOURCE_NOT_FOUND)
unable to connect with SMB workgroup

Listing 556 - Connecting to the SMB share on SHARES, without any explicit forwarding.

Great! We're now connecting to SHARES transparently, as we are on the same network and have direct access. In this section, we used sshuttle to create a VPN-like environment. We were then able to connect transparently to SHARES from our Kali machine, though we were on the same network as PGDATABASE1.

### 18.4 Port Forwarding with Windows

This Learning Unit covers the following Objectives:
- Use ssh.exe and Plink to create port forwards for Windows
- Understand port forwarding with Netsh

So far in this Module, we've discussed the mechanics of port redirection and tunneling using Linux-based tools. However, we will often encounter Windows hosts in large networks that require us to practice port forwarding strategies. Frankly, there are several ways to port forward and tunnel on Windows, a few of which we'll cover in this Learning Unit.

#### ssh.exe

The OpenSSH client has been bundled with Windows by default since version 1803 (April 2018).⁵ and has been available as Feature-on-demand since 1709 (Windows 10 Fall Creators Update).⁶. On Windows versions with SSH installed, we will find scp.exe, ssh.exe, along with other utilities in %systemroot%\System32\OpenSSH location by default.

The fact that the SSH client is compiled for Windows means that we can only connect to Windows SSH servers. We can connect to any SSH server we want as long as we have the credentials. Let's practice by creating a remote dynamic port forward from MULTSERVER03 (Windows machine) to our Kali machine. In this scenario, only RDP port is open on MULTSERVER03. We can RDP in, but we can't bind any other ports to the WAN interface. Once we have our lab set, it should appear as:

![](img/336dea891e7464f18ad6442619ced4_597_0.png)

Figure 253: The SSH remote port forward setup using the Windows OpenSSH client

We'll use `rdp_admin` credentials we found earlier to RDP into our Kali machine. We'll use `ssh.exe` to create a remote dynamic port forward connection to our Kali machine. We can then use that to connect to the PostgreSQL database service on PGDATABASE1.

First, let's start by sure the SSH server is running on our Kali machine.

```
kali@kali:~ sudo systemctl start ssh
[sudo] password for kali:
```

⁵(Yosef Durr, 2018), https://devblogs.microsoft.com/commandline/windows101803/#openssh-based-client-and-server
⁶(Joey Aiello, 2017), https://devblogs.microsoft.com/powershell/using-the-openssh-beta-in-windows-10-fall-creators-update-and-windows-server-1709/

Listing 557 - Starting SSH server on the Kali machine.

```
kali@kali:~
We can use xfreeerdp from FreeRDP9 to connect to the RDP on MULTSERVER03.
kali@kali:~$ xfreeerdp /u:rdp_admin /p:password@v:192.168.50.64
[15:46:35:297][48172:48173][WARN](com.freerdp.crypto) - Certificate verification failed 'self signed certificate (1)' at stack position 0
[15:46:35:297][48172:48173][WARN](com.freerdp.crypto) - CN = MULTSERVER03
[15:46:35:297][48172:48173][WARN](com.freerdp.crypto) - CERTIFICATE MISMATCH
[15:46:35:301][48172:48173][ERROR](com.freerdp.crypto) - ========================================
[15:46:35:301][48172:48173][ERROR](com.freerdp.crypto) - The hostname used for this connection (192.168.50.64) does not match the given in the certificate:
[15:46:35:301][48172:48173][ERROR](com.freerdp.crypto) - Common Name (CN): MULTSERVER03
[15:46:35:301][48172:48173][ERROR](com.freerdp.crypto) - Subject: CN = MULTSERVER03
Thumbprint: f5:42:78:b6:78:b6:54:85:75:c2:3c:74:56:fa:b3:ed:f0:87:9e:ee:9a:ba:e2:19
ca in your store, or it has expired.
Please look at the OpenSSL documentation on how to add a private CA to the store.
Do you trust the certificate? (Y/T/N) y
[15:46:38:728][48172:48173][ERROR](com.winpr.timezone) - Unable to find a unix timezone: US/Eastern
[15:46:35:238][48172:48173][INFO](com.freerdp.gdi) - Local framebuffer format
PIXEL_FORMAT_BGR32
[15:46:39:539][48172:48173][INFO](com.freerdp.gdi) - Remote framebuffer format
PIXEL_FORMAT_BGR32
[15:46:40:175][48172:48173][INFO](com.freerdp.channels.rdpsnd.client) - [static]
loaded failed backend for rdpsnd
[15:46:41:176][48172:48173][INFO](com.freerdp.channels.dryncvc.client) - Loading
Dynamic Virtual Channel rdgfx
```

Listing 558 - Connecting to the RDP server on MULTSERVER03 using xfreerdp.

Once we have a connection open, we can open a cmd.exe window and determine whether SSH is on the box using ssh.
