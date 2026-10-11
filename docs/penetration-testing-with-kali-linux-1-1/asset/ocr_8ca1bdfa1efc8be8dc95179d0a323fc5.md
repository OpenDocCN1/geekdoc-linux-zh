Take a moment to understand this admittedly complex traffic flow before proceeding. Port forwarding with encapsulation can be complicated because we have to consider firewall rules, protocol limitations, and both inbound and outbound port allocations. It often helps to pause and write a map or flow chart like the one shown in Figure 304 below before executing the actual commands. This process is complicated enough without attempting to figure out both logic flow and syntax simultaneously.

![](bbox=[0.14, 0.24, 0.85, 0.56])

To begin building our tunnel, we will create a local SSH-based port forward between our compromised Linux machine and the Windows remote desktop target. Remember, protocol does not matter here (SSH is allowed) as this traffic is unaffected by deep packet inspection on the internal network.

To do this, we will create a local forward (-L) from this machine (127.0.0.1) and will log in as **student**, using the new password we created post-exploitation. We will forward all requests on port 8888 (0.0.0.0:8888) to the Windows Server's remote desktop port (192.168.1.110:3389):

```
www-data@debian:~$ ssh -L 0.0.0.0:8888:192.168.1.110:3389 student@127.0.0.1
ssh -L 0.0.0.0:8888:192.168.1.110:3389 student@127.0.0.1
Could not create directory '/var/www/.ssh'.
The authenticity of host '127.0.0.1 (127.0.0.1)' can't be established.
ECDSA key fingerprint is SHA256:RdJ3nCwLcxEG+c6nSHi13N6QykXAbDJkRma3cLtknnuJ0.
Are you sure you want to continue connecting (yes/no)?
 yes
Failed to add the host to the list of hosts (/var/www/.ssh/known_hosts).
student@127.0.0.1's password:  lab
...

student@debian:~$ ss -antp | grep "8888"
```