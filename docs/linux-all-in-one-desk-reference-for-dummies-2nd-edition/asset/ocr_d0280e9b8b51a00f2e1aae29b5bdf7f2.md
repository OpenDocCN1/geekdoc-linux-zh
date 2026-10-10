A user who wants to log in using SSH can simply use the ssh command. For example, here is what I type on one system to log into another using SSH:

```
ssh 192.168.0.4 -1 naba
```

where 192.168.0.4 is the IP address of the other Linux system. SSH then displays a message:

> The authenticity of host '192.168.0.4 (192.168.0.4)' can't be established.
> RSA key fingerprint is 7b:79:f2:d8:8c:54:00:a6:94:ec:fa:8e:7f:c9:ad:66.
> Are you sure you want to continue connecting (yes/no)?

I type yes and press Enter. SSH then adds the host to its list of known hosts and prompts me for my password on the other Linux system:

```
naba@192.168.0.4's password:
```

After I enter my password, I have a secure login session with that system. I can also log in to this account with the following equivalent command:

```
ssh naba@192.168.0.4
```

If I simply want to copy a file securely from another system on the LAN (identified by its IP address 192.168.0.4), I can use scp like this:

```
scp 192.168.0.4:/etc/X11/xorg.conf .
```

This command prompts for my password and securely copies the /etc/X11/xorg.conf file from the 192.168.0.4 host to the system from which I type the scp command, as follows:

```
naba@192.168.0.4's password: (I type my password.)
xorg.conf 100% 2814 2.8KB/s 00:00
```

# ## Setting Up Simple Firewalls

A firewall is a network device or host with two or more network interfaces — one connected to the protected internal network and the other connected to unprotected networks, such as the Internet. The firewall controls access to and from the protected internal network.

If you connect an internal network directly to the Internet, you have to make sure that every system on the internal network is properly secured — which can be nearly impossible because a single careless user can render the entire internal network vulnerable. A firewall is a single point of connection to the Internet: You can direct all your efforts toward making that firewall system a