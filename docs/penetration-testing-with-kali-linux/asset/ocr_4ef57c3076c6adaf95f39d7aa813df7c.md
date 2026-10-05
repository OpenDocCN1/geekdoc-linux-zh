# OffSec

Penetration Testing with Kali Linux

172.16.50/24 dev ens24 proto kernel link src 172.16.50.215
172.16.50/24 via 172.16.50.254 dev ens24 proto static

Listing 535 - Enumerating network routes on PGDATBASE01.

We find that PGDATBASE01 is attached to another subnet, in this 172.16.50/24 range. We do not find a scanner installed on PGDATBASE01; however, we can still do initial reconnaissance with the tools that are available.

Let's write a Bash loop to scan for hosts with an open port 445 on the /24 subnet. We can use Netcat to make the connections, the -z flag for checking a listening port without sending data, -v for verbosity, and -w 1 to ensure a lower time-timeout.

```
database_admin@pgdatabase01:-$ for i in $(seq 1 254); do nc -zv -w 1 172.16.50.$i 445; done
< (seq 1 254); done
nc: connect to 172.16.50.151 445 (tcp) timed out: Operation in progress
nc: connect to 172.16.50.216 445 (tcp) failed: Connection refused
Connection to 172.16.50.217 445 [tcp/microsoft-ds] succeeded!
c: connect to 172.16.50.218 445 (tcp) timed out: Operation in progress
database_admin@pgdatabase01:-$
```

Listing 536 - Using a bash loop with Netcat to scan for port 445 in the newly-found subnet.

Most of the connections we make, suggesting that there's nothing there. In contrast, we'll notice PGDATBASE01 (172.16.50.215) actively refused the connection. We also find that there is a host on the subnet, which has TCP port 445 open: 172.16.50.217!

We want to enumerate the SMB service on this host. If we find anything, we want to download it to our Kali machine for inspection. There are at least two ways we could do this:

One way is to use whatever built-in tools we find on PGDATBASE01. However, if we find anything, we would have to download it to PGDATBASE01, then transfer it back to our Kali machine. CONFLUENCE01, then would create a tedious manual data transfer.

The alternative is to use SSH port forwarding. We could create an SSH connection to CONFLUENCE01 as part of that connection, we could create an SSH local port forward. This would listen on port 445 on the WAN interface of CONFLUENCE01, forwarding packets through the SSH tunnel of CONFLUENCE01 and directly to the SMB service we found. We could then connect to the listening port on CONFLUENCE01 directly from our Kali machine.

> In this scenario, there is no firewall preventing us from accessing ports that we bind on the WAN interface of CONFLUENCE01. In later sections, we will put the firewall up, and use more advanced techniques to traverse this boundary.

Now, we should kill our existing SSH connection to PGDATBASE01. We will set up a new connection with new arguments to establish the SSH port forward.

PWK - Copyright © 2023 OffSec Services Limited. All rights reserved.

581