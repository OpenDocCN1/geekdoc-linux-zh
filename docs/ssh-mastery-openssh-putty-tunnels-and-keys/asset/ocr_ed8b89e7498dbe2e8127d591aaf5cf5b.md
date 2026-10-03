illustrates dynamic port forwarding.

![](bbox=[0.145, 0.105, 0.41, 0.185])

Figure 9-3: Dynamic Port Forwarding Data Flow

When the underlying SSH session dies, all ports stop being forwarded.

Chapter 10 offers suggestions for keeping SSH sessions alive.

With these possibilities, it’s easy to see why sysadmins love SSH, and why many corporate security departments forbid it.

# Privileged Ports and Forwarding

On Unix-like systems, TCP ports below 1024 are reserved for system use. Only root can bind to these ports. As an unprivileged user, you can attach the local end of your SSH port forwarder to any port above 1024. Forwarding a reserved port requires using SSH as root. Performing routine tasks as root is poor practice, so don’t do it without a really good reason.

Only the side of the connection that is attaching to a privileged port needs to run as root. If you’re binding a reserved port on the client, run the client as root but to log into the server as a regular user. If you’re binding a reserved port on the server, you’ll need to log into the server as root. In the latter case, it’s a better idea to change the port so you don’t have to login directly as root.

Microsoft systems do not implement privileged ports. Anyone can bind to any open port on the system. The absence of port restrictions creates all sorts of potentially amusing security issues, but it does make forwarding low-numbered reports no more difficult than forwarding any other port. You never need to run PuTTY as root.

# Local Port Forwarding

Before setting up local port forwarding, verify that normal SSH works. Then figure out what service you want to forward, and what port that service runs on. Some typical choices are 80 (HTTP), 25 (SMTP), and 110 (POP3). The services that usually run on these ports are not normally encrypted.

Now choose a local port you want to use for the forwarding. Some clients work well when run on any port. Almost any mail client lets you set a TCP port to check POP 3 on. Others… don’t. Websites frequently choke if you change the port number. If you don’t know how the protocol behaves when forwarded from one port to another, try it on a test server and see.

For our local port forwarding examples, we’ll forward port 8080 on my client to port 80 on the server sloth. Now that TLS certificates are free, why would you