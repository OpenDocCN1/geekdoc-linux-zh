
![](img/ec25e59d75726b7041242a56d3376832_593_0.png)

This is one of the more basic scenarios in this module. Be sure to take time to complete the exercises and understand these concepts before proceeding.

## 20.1.1.1 Exercises

- Connect to your dedicated Linux lab client and run the `clear_rules.sh` script from `/root/port_forwarding_and_tunneling/` as root.
- Attempt to replicate the port-forwarding technique covered in the above scenario.

## 20.2 SSH Tunneling

The SSH protocol<sup>591</sup> is one of the most popular protocols for tunneling and port forwarding.<sup>592</sup> This is due to its ability to create encrypted tunnels within the SSH protocol, which supports bi-directional communication channels. This obscure feature of the SSH protocol has far-reaching implications for both penetration testers and system administrators.

### 20.2.1 SSH Local Port Forwarding

SSH local port forwarding allows us to tunnel a local port to a remote server using SSH as the transport protocol. The effects of this technique are similar to rinetd port forwarding, with a few twists.

<sup>591</sup> (SSH Communications Security, 2018), https://www.ssh.com/ssh/protocol/

<sup>592</sup> (Trackets Blog, 2017), https://blog.trackets.com/2014/05/17/ssh-tunnel-local-and-remote-port-forwarding-explained-with-examples.html

![](img/ec25e59d75726b7041242a56d3376832_594_0.png)

Let’s take another scenario into consideration. During an assessment, we have compromised a Linux-based target through a remote vulnerability, elevated our privileges to root, and gained access to the passwords for both the root and student users on the machine. This compromised machine does not appear to have any outbound traffic filtering, and it only exposes SSH (port 22), RDP (port 3389), and the vulnerable service port, which are also allowed on the firewall.

After enumerating the compromised Linux client, we discover that in addition to being connected to the current network (10.11.0.x), it has another network interface that seems to be connected to a different network (192.168.1.x). In this internal subnet, we identify a Windows Server 2016 machine that has network shares available.

To simulate this configuration in our lab environment, we will run the `ssh_local_port_forwarding.sh` script from our dedicated Linux client:

```bash
root@debian:~# cat /root/port_forwarding_and_tunneling/ssh_local_port_forwarding.sh
#!/bin/bash

# Clear iptables rules
iptables -P INPUT ACCEPT
iptables -P FORWARD ACCEPT
iptables -P OUTPUT ACCEPT
iptables -F
iptables -X

# SSH Scenario
iptables -F
iptables -P INPUT DROP
iptables -P FORWARD DROP
iptables -A INPUT -i lo -j ACCEPT
iptables -A INPUT -m state --state ESTABLISHED,RELATED -j ACCEPT
iptables -A INPUT -p tcp --dport 3389 -m state --state NEW -j ACCEPT
iptables -A INPUT -p tcp --dport 22 -m state --state NEW -j ACCEPT
iptables -A INPUT -p tcp --dport 8080 -m state --state NEW -j ACCEPT
iptables -A INPUT -i lo -j ACCEPT
root@debian:~# /root/port_forwarding_and_tunneling/ssh_local_port_forwarding.sh
```

> Listing 632 - Content of the ssh_local_port_forwarding.sh script

In such a scenario, we could move the required attack and enumeration tools to the compromised Linux machine and then attempt to interact with the shares on the 2016 server, but this is neither elegant nor scalable. Instead, we want to interact with this new target from our Internet-based Kali attack machine, pivoting through this compromised Linux client. This way, we will have access to all of the tools on our Kali attack machine as we interact with the target.

This will require some port-forwarding magic, and we will use the ssh client’s local port forwarding feature (invoked with `ssh -L`) to help with this.

The syntax is as follows:

```bash
ssh -N -L [bind_address:]port:host:hostport [username@address]
```

> Listing 633 - Command prototype for local port forwarding using SSH

Inspecting the manual of the ssh client (`man ssh`), we notice that the -L parameter specifies the port on the local host that will be forwarded to a remote address and port.

In our scenario, we want to forward port **445** (Microsoft networking without NetBIOS) on our Kali machine to port **445** on the Windows Server 2016 target. When we do this, any Microsoft file sharing queries directed at our Kali machine will be forwarded to our Windows Server 2016 target. This seems impossible given that the firewall is blocking traffic on TCP port **445**, but this port forward is tunneled through an SSH session to our Linux target on port **22**, which is allowed through the firewall. In summary, the request will hit our Kali machine on port **445**, will be forwarded across the SSH session, and will then be passed on to port **445** on our Windows Server 2016 target.

If done correctly, our tunneling and forwarding setup will look something like Figure 298:

![](img/ec25e59d75726b7041242a56d3376832_595_0.png)

To pull this off, we will execute an ssh command from our Kali Linux attack machine. We will not technically issue any ssh commands (`-N`) but will set up port forwarding (with `-L`), bind port **445** on our local machine (**9.0.0.0:445**) to port **445** on the Windows Server (**192.168.1.110:445**) and do this through a session to our original Linux target, logging in as student (**student@10.11.0.128**):

```bash
kali@kali:~$ sudo ssh -N -L 9.0.0.0:445:192.168.1.110:445 student@10.11.0.128
student@10.11.0.128's password:
```

> Listing 634 - Forwarding TCP port 445 on our Kali Linux machine to TCP port 445 on the Windows Server 2016

At this point, any incoming connection on the Kali Linux box on TCP port **445** will be forwarded to TCP port **445** on the 192.168.1.110 IP address through our compromised Linux client.

Before testing this, we need to make a minor change in our Samba configuration file to set the minimum SMB version to SMBv2 by adding `"min protocol = SMB2"` to the end of the file as shown in Listing 635. This is because Windows Server 2016 no longer supports SMBv1 by default.

```bash
kali@kali:~$ sudo nano /etc/samba/smb.conf

kali@kali:~$ cat /etc/samba/smb.conf
...
Please note that you also need to set appropriate Unix permissions
# to the drivers directory for these users to have write rights in it
;
write list = root, @lpadmin

min protocol = SMB2

kali@kali:~$ sudo /etc/init.d/smbd restart
[ ok ] Restarting smbd (via systemctl): smbd.service.
```

*Listing 635 - Updating Samba from SMBv1 to SMBv2 communications*

Finally, we can try to list the remote shares on the Windows Server 2016 machine by pointing the request to our Kali machine.

We will use the smbclient utility, supplying the IP address or NetBIOS name, in this case our local machine (`-L 127.0.0.1`) and the remote user name (`-U Administrator`). If everything goes according to plan, after we enter the remote password, all the traffic on that port will be redirected to the Windows machine and we will be presented with the available shares:

```bash
kali@kali:~# smbclient -L 127.0.0.1 -U Administrator
Unable to initialize messaging context
Enter WORKGROUP\Administrator's password:

Sharename    Type       Comment
---------    ----       -------
ADMIN$       Disk       Remote Admin
C$          Disk       Default share
Data         Disk
IPC$         IPC        Remote IPC
NETLOGON     Disk       Logon server share
SYSVOL       Disk       Logon server share
Reconnecting with SMB1 for workgroup listing.

Server     Comment
---------    -------

Workgroup    Master
---------    -------
```

*Listing 636 - Listing net shares on the Windows Server 2016 machine through local port forwarding*

Not only was the command successful, but since this traffic was tunneled through SSH, the entire transaction was encrypted. We can use this port forwarding setup to continue to analyze the target server via port 445, or forward other ports to conduct additional reconnaissance.

### 20.2.1.1 Exercises

- Connect to your dedicated Linux lab client and run the `clear_rules.sh` script from `/root/port_forwarding_and_tunneling/` as root.
- Run the `ssh_local_port_forwarding.sh` script from `/root/port_forwarding_and_tunneling/` as root.
