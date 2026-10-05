# OffSec

Penetration Testing with Kali Linux

WAN

DMZ

?????

ssh client

ssh server

CONFLUENCE01

PGDATABASE01

KALI-MACHINE

?????

Figure 246: How we want our SSH local port to work in the lab, at a high level

In this diagram, we listen on TCP port 4455 on CONFLUENCE01. Packets sent to that port are pushed by the SSH client software on CONFLUENCE01 through the SSH tunnel. The SSH server software on PGDATABASE01 forwards them to SSH to TCP port 445 on the newly-found host.

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
ECDSA key fingerprint is SHA256:K9x2nuxXQib/JtYn/YmDBV8Ky7kTeEqieIyt1ytH4
Are you sure you want to continue connecting (no/[fingerprint])?
yes

Failed to add the host to (/home/confluence/.ssh/known_hosts),
dabase_admin@10.4.50.215's password:

> 915 (Wikipedia, 2022), https://en.wikipedia.org/wiki/TTY

PWK - Copyright © 2023 OffSec Services Limited. All rights reserved.

579