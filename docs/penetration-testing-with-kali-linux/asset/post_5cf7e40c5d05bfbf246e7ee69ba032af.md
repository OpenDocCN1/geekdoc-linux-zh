
# OffSec

Penetration Testing with Kali Linux

Are you sure to continue connecting (yes/no/[fingerprint]) yes
Warning: Permanently added '[192.168.50.63]:2222' (ED25519) to the list of known hosts.
database_admin@192.168.50.63 password:
Welcome to Ubuntu 20.04.4 LTS (GNU/Linux 5.4.0-122-generic x86_64)

* Documentation: https://help.ubuntu.com
* Management: https://landscape.canonical.com
* Support: https://ubuntu.com/advantage

System information as of Thu 18 Aug 2022 11:43:07 UTC

| System load: 0.1 | Processes: 241 |
| Usage of / 59.3 of 7.77GB | Users logged in: 1 |
| Memory usage: 16% | IPv4 address for ens192: 10.4.50.215 |
| Swap usage: 0% | IPv4 address for ens224: 172.16.50.215 |

@ updates can be applied immediately.

Failed to connect to https://changelogs.ubuntu.com/meta-release-lts. Check your Internet connection or proxy settings

The programs included with the Ubuntu system are free software; the exact distribution terms for each program are described in the individual files in /usr/share/doc/**copyright.

Ubuntu comes with ABSOLUTELY NO WARRANTY, to the extent permitted by applicable law.

Listing 532 - Connecting to SSH server on PGDATABASE01, the port forward on CONFLUENCE01.

Success! The database_admin credentials have been reviewed here. We have managed to connect to the SSH server on PGDATABASE01 using the credentials for database_admin we found in the PostgreSQL through the port forward we set up on CONFLUENCE01 Socat.

In this Learning Unit, we created some port forwards using Socat. This allowed us to gain deeper access within a network by leveraging our existing access to a compromised host.

It should also be noted that Socat is not the only way to create port forwards on *NIX hosts. There are several alternatives, of note:

- rinetd⁹⁴ is an option that runs as a daemon. This makes it better for longer-term port forwarding configurations, but is slightly unwieldy for temporary port forwarding solutions.

- We combine Netcat and a FIFO⁹⁵ named pipe file to create a port forward ⁶⁶⁴ (Thomas Boutell and Sam Hocever, 2022), https://github.com/samhocever/rinet

⁵ (Linux manual page, 2022), https://man.7/man-pages/man7/fifo.7 html

⁶ (holly, 2015), https://github.com/holly/65d2dd9aadd35e8b2fd5

If we have privileges, we can use iptables to create port forwards. The specific iptables forwarding setup for a given host will likely depend on the configuration already in place. To be able to forward packets in Linux also requires enabling forwarding on the interface we want to forward on by writing "1" to /proc/sys/net/ipv4/conf/[interface]/forwarding (if it's not already configured to it).

## 18.3 SSH Tunneling

This Learning Unit covers the fundamentals of SSH tunneling

1. Learn the fundamentals of SSH tunneling
2. Use SSH local, dynamic, remote, and remote dynamic port forwarding techniques
3. Understand the process of using sshuttle

At a high-level, tunneling describes the act of encapsulating one kind of data stream within another as it travels across a network. Protocols called tunneling protocols^907 are designed specifically to do this. Secure Shell^908 is an example of one of these protocols.^909

SSH was initially developed to give administrators the ability to log into their servers through an encrypted connection. Before SSH, tools such as rsh, login^910 and Telnet^911 provided remote administration capabilities, but over an unencrypted connection.

In the background of each SSH connection, all commands, passwords, and data are transported through an encrypted tunnel built using SSH protocol. The SSH protocol is primarily a tunneling protocol, so it's possible to pass any kind of data through an SSH connection. For that reason, tunneling can be built into most SSH tunnels.

Another great benefit of SSH tunneling is how easily it can be built into the background traffic of network environments. SSH is often used by network administrators for legitimate administration purposes, and flexible port forwarding sets in restrict network situations. It is also common to find SSH client software already installed on Linux hosts, or even SSH servers running on Windows. In network environments that are not heavily monitored, SSH traffic will not seem anomalous, and SSH traffic will look much like regular administrative traffic. Its contents cannot be easily monitored.

In most official documentation, tunneling data through an SSH connection is referred to as port forwarding.^913 Different SSH software will provide different port forwarding capabilities. We can use common SSH port forwarding types offered by OpenSSH in this Learning Unit.

> ^907 (Wikipedia, 2019), https://en.wikipedia.org/wiki/Tunneling_protocol
> 908 (Wikipedia, 2022), https://en.wikipedia.org/wiki/Secure_Shell
> 909 (SSH, 2018), https://www.ssh.com/ssh/protocol/
> 910 (Wikipedia, 2022), https://en.wikipedia.org/wiki/Berkeley_commands
> 911 (Wikipedia, 2022), https://en.wikipedia.org/wiki/Telnet
> 912 (OpenSSH, 2022), https://www.openssh.com/
> 913 (SSH, 2022), https://www.ssh.com/academy/ssh-tunneling-example#what-is-ssh-port-forwarding-aka-ssh-tunneling?

SSH port forwarding can be a hugely powerful tool in any situation, but it can also be very useful option for attackers working in restrictive environments.

### 18.3.1 SSH Local Forwarding

Let's recall the first port forwarding from the Socat scenario. We set up Socat to listen on TCP port 2345 on the WAN interface of CONFLUENCE01. Packets received on that port were forwarded to TCP port 5432 on PGDATABASE01. We used this to connect to our Kali machine, through CONFLUENCE01, to the PostgreSQL service on PGDATABASE01. The crucial thing to notice in this case is that listening and forwarding were both from the same host (CONFLUENCE01).

SSH local port forwarding adds a small twist. With local port forwarding, packets are not forwarded by the same host. Instead, an SSH connection is made between two hosts (an SSH client and an SSH server), a listening port is opened by the SSH client, and all packets received on this port are tunneled through the SSH connection to the SSH server. The packets are then forwarded by the SSH server to the socket we specify.

This concept might seem a bit abstract at the moment. We can understand it better by getting up a local port forward. Let's reconsider the previous scenario with a slight modification: Socat is no longer available on CONFLUENCE01. We still have the credentials we previously cracked from the Confluence database, and there is still no firewall preventing us from connecting to the ports we bind on CONFLUENCE01.

With the database_admin credentials, we will log in to PGDATABASE01 and find that it's attached to another subnet. We find a host with a Server Message Block (SMB) server open (on TCP port 445) in that subnet. We will be able to connect to that server and download what we find to our Kali machine.

In this type of scenario, we'll plan to create an SSH port forward as part of our SSH connection from CONFLUENCE01 to PGDATABASE01. We will bind a listening port on the WAN interface of CONFLUENCE01. All packets sent to that port will be forwarded through the SSH tunnel. PGDATABASE01 will then forward these packets towards the SMB port on the new host.

The following diagram illustrates our setup:

| WAN | DMZ | |
| :--- | :--- | :--- |
| | ssh client | ssh server |
| | CONFLUENCE01 | PGDATABASE01 | |

Figure 246: How we want our SSH local port to work in the lab, at a high level

In this diagram, we listen on TCP port 4455 on CONFLUENCE01. Packets sent to that port are pushed by the SSH client software on CONFLUENCE01 through the SSH tunnel. The SSH server software on PGDATABASE01 forwards them to TCP port 445 on the newly-found host.

Let's set up our lab environment just like this. A VM group for following along is provided at the bottom of this section.

As before, we can get a shell on CONFLUENCE01 using a cURL one-liner exploit for CVE-2022-26134. We can no longer use Socat to create a port forward that allows us to use SSH to PGDATABASE01 our Kali machine. However, in this case, we can use SSH directly from CONFLUENCE01 to PGDATABASE01.

We can't create our SSH local port forward yet, we need to know exactly which IP address and port we want the packets forwarded to. Before we create the port forward with SSH connection, let's use SSH into PGDATABASE01 to start enumerating.

In our shell from CONFLUENCE01, we'll make sure that TTY functionality is using the Python 3's pty module. We can then SSH into PGDATABASE01 with the database_admin credentials.

```
confluence01@/opt/atlassian/confluence/bin$ python 3 -c 'import pty;
ty.spawn("/bin/bash")'
<$ python 3 -c 'import pty; pty.spawn("/bin/bash")'
confluence01@/opt/atlassian/confluence/bin$ ssh database_admin@10.4.50.215
<shell/confluence@bin5$ ssh database_admin@10.4.50.215
Could not create directory "/home/confluence/.ssh".
```

The authenticity of host '10.4.50.215' can't be established.
ECDSA key fingerprint is SHA256:K9x2nuxXQib/JtYn/YmDBV8Ky7kTeEqIyt1yt4
Are you sure you want to continue connecting (no/[fingerprint])?
yes

Failed to add the host to (/home/confluence/.ssh/known_hosts),
dabase_admin@10.4.50.215's password:
