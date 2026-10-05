# OffSec

If we have privileges, we can use iptables to create port forwards. The specific iptables forwarding setup for a given host will likely depend on the configuration already in place. To be able to forward packets in Linux also requires enabling forwarding on the interface we want to forward on by writing "1" to /proc/sys/net/ipv4/conf/[interface]/forwarding (if it's not already configured to it).

# 18.3 SSH Tunneling

This Learning Unit covers the fundamentals of SSH tunneling

+   1. Learn the fundamentals of SSH tunneling
2. Use SSH local, dynamic, remote, and remote dynamic port forwarding techniques
3. Understand the process of using sshuttle

At a high-level, tunneling describes the act of encapsulating one kind of data stream within another as it travels across a network. Protocols called tunneling protocols^907 are designed specifically to do this. Secure Shell^908 is an example of one of these protocols.^909

SSH was initially developed to give administrators the ability to log into their servers through an encrypted connection. Before SSH, tools such as rsh, login^910 and Telnet^911 provided remote administration capabilities, but over an unencrypted connection.

In the background of each SSH connection, all commands, passwords, and data are transported through an encrypted tunnel built using SSH protocol. The SSH protocol is primarily a tunneling protocol, so it's possible to pass any kind of data through an SSH connection. For that reason, tunneling can be built into most SSH tunnels.

Another great benefit of SSH tunneling is how easily it can be built into the background traffic of network environments. SSH is often used by network administrators for legitimate administration purposes, and flexible port forwarding sets in restrict network situations. It is also common to find SSH client software already installed on Linux hosts, or even SSH servers running on Windows. In network environments that are not heavily monitored, SSH traffic will not seem anomalous, and SSH traffic will look much like regular administrative traffic. Its contents cannot be easily monitored.

In most official documentation, tunneling data through an SSH connection is referred to as port forwarding.^913 Different SSH software will provide different port forwarding capabilities. We can use common SSH port forwarding types offered by OpenSSH in this Learning Unit.

> ^907 (Wikipedia, 2019), https://en.wikipedia.org/wiki/Tunneling_protocol
908 (Wikipedia, 2022), https://en.wikipedia.org/wiki/Secure_Shell
909 (SSH, 2018), https://www.ssh.com/ssh/protocol/
910 (Wikipedia, 2022), https://en.wikipedia.org/wiki/Berkeley_r-commands
911 (Wikipedia, 2022), https://en.wikipedia.org/wiki/Telnet
912 (OpenSSH, 2022), https://www.openssh.com/
913 (SSH, 2022), https://www.ssh.com/academy/ssh-tunneling-example#what-is-ssh-port-forwarding-aka-ssh-tunneling?