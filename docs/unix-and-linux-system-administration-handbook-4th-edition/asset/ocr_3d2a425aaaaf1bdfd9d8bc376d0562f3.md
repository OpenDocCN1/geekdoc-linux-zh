also pass -o "VerifyHostKeyDNS yes" on the ssh command line when first accessing a new system.

SSH has a couple of ancillary functions that are useful for system administrators. One of these is the ability to tunnel TCP connections securely through an encrypted SSH channel, thereby allowing connectivity to insecure or firewalled services at remote sites. This functionality is ubiquitous among SSH clients and is simple to configure. Exhibit A shows a typical use of an SSH tunnel and should help clarify how it works.

# Exhibit A An SSH tunnel for RDP

![](bbox=[0.22, 0.4, 0.9, 0.65])

In this scenario, a remote user wants to establish an RDP (remote desktop) connection to a Windows system on the enterprise network. Access to that host or to port 3389 is blocked by the firewall, but since the user has SSH access, he can route his connection through the SSH server.

To set this up, the user logs in to the remote SSH server with ssh. On the ssh command line, he specifies an arbitrary (but specific; in this case, 9989) local port that ssh should forward through the secure tunnel to the remote Windows machine's port 3389. (For the standard OpenSSH implementation, the option to request this behavior is simply -L localport:remotemachine:remoteport.) All source ports in this example are marked as random since programs choose an arbitrary port from which they initiate connections.

To access the Windows machine's desktop, the user then opens the remote desktop client (here, rdesktop) and enters localhost:9989 as the address of the server to connect to. The local ssh receives the connection on port 9989 and tunnels the traffic over the existing connection to the remote sshd. In turn, sshd forwards the connection to the Windows host.

Of course, tunnels such as these can be intentional or unintentional back doors as well. System administrators should use tunnels with caution and should also watch for unauthorized misuse of this facility by users.