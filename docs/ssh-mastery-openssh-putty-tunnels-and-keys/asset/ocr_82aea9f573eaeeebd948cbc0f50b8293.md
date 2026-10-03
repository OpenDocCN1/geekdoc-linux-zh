a firewall. The firewall might be my home NAT device, or my employer’s industrial-grade corporate firewall cluster. Remote forwarding lets me use my client to give an SSH server outside the network a way to connect to a host inside the firewall, despite any firewall rules to the contrary. This might be my invaluable emergency back door into my own network, or it might violate my employer’s security policy. Or, better still: both!

Note that you cannot bind a forwarded port to the SSH server’s public-facing IP addresses unless the server is specifically configured to permit this with the GatewayPorts keyword. See “Restricting Port Forwarding” later this chapter.

# OpenSSH Remote Forwarding

Configure remote port forwarding with the -R flag.

```
$ ssh -R remoteIP:remoteport:localIP:localport hostname
```

If you don’t specify an IP address to attach to on the SSH server, SSH attaches to 127.0.0.1. You can skip the first argument in this case, making the command:

```
$ ssh -R remoteport:localIP:localport hostname
```

I want to connect port 2222 on the SSH server sloth to port 22 on my workstation, using the localhost address on both sides.

```
$ ssh -R 2222:localhost:22 sloth
```

My client connects to the server and gives me a command prompt. As long as that SSH session remains open, another user on sloth could SSH to my workstation by connecting to port 2222.

```
sloth$ ssh -p 2222 localhost
```

Poof! A new SSH connection into my workstation, tunneled inside my existing SSH session. This new session would show up in the client log as a new connection, originating from the localhost. You really need to trust the people who have accounts on your systems when setting up remote port forwarding. Anyone who can access your system’s localhost address can use the port forwarding. I would never use remote port forwarding on an SSH server I didn’t wholly trust.

If you want to establish remote port forwarding every time you connect to a server, use the RemoteForward keyword in ssh_config.

```
RemoteForward server-IP:server-port client-IP:client-port
```

Once again, this resembles port forwarding on the command line, but the middle colon is missing. Here I set up this same port forwarding in the configuration file.

```
Host sloth.mwl.io
RemoteForward localhost:2222 localhost:22
```

The RemoteForward keyword most commonly appears with a Host statement, unless you want to perform remote forwarding on every host you connect to.