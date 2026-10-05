# OffSec

884 confirms that the machine is running Ubuntu 22.04 as we've identified via the OpenSSH service version.

Next, we'll review the network interfaces.

```
Interfaces
# symbolic names for networks, see networks(5) for more information
link-local 169.254.0.1
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noque state UNKNOWN group default qlen 1000
	tilink/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
	inet 127.0.0.1/8 scope lo
	valid lft forever preferred_lft forever
	inets ::1/128 scope host
	valid lft forever preferred_lft forever
2: ens192:<BROADCAST,MULTICAST,LOWER_UP> mtu 1500 qdisc fq_cod state UP group default qlen 1000
	tilink/eth0:50:56:25:64 alname enp0
	inet 192.168.0.244/24 brd 192.168.0.255 scope global ens192
	valid lft forever preferred_lft forever
	inet6 fe80::fe56:fffe/64 scope link
	valid lft forever preferred_lft forever
```

885 - Network interfaces

885 shows only one network interface apart the loopback interface. This means the target machine is not connected to the internal network and we cannot use it as a pivot point.

Since we have already enumerated MAILSV1 without any actionable results and this machine is not connected to the internal network, we have to discover sensitive information, such as credentials, to get a foothold in the internal network. To obtain files and data from other users and the system, we are elevating our privileges priority.

The interesting result from linPEAS contains an interesting piece of information regarding commands executable with sudo.

```
Checking '-l', /etc/sudoers, and /etc/sudoers.d
https://book.hackacks.xyz/linux-hardening/privilege-escalation-sudo-suid
Matching Defaults for entries daniela on websrv1:
env_rest,mail_passwd,
secure_path=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/snap/bin
```

User daniela may run the following commands on websrv1:

```
(ALL) PASSWD: /usr/bin/git
```

886 - Sudo commands for daniela

Listing 886 shows that daniela can run /usr/bin/git with sudo privileges without entering a password.

Before we try to leverage this finding into privilege escalation, let's find linPEAS results. We might miss some crucial findings.

The next interesting is Analyzing WordPress Files, which contains a clear-text password used for database access.