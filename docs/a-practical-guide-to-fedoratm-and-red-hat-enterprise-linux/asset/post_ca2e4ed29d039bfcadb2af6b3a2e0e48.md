
## Debug the client
If entries in these files do not help solve the problem, try connecting with the `-v` option (either `ssh` or `scp` — the results should be the same). OpenSSH displays a lot of debugging messages, one of which might help you figure out what the problem is. You can use a maximum of three `-v` options to increase the number of messages that OpenSSH displays.

```
$ ssh -v plum
OpenSSH_5.2p1, OpenSSL 1.0.1e-fips  11 Feb 2013
debug1: Reading configuration data /etc/ssh_config
debug1: /etc/ssh/ssh_config line 50: Applying options for *
debug1: Connecting to plum [192.168.266.181] port 22.
debug1: Connection established.
debug1: identity file /home/sam/.ssh/id_rsa type 1
debug1: identity file /home/sam/.ssh/id_rsa-cert type -1
...
debug1: Host 'plum' is known and matches the RSA host key.
debug1: Found key in /home/sam/.ssh/known_hosts:1
debug1: ssh_rsa_verify: signature correct
...
debug1: Authentications that can continue: publickey,gssapi-keyex,gssapi-with-mic,password
debug1: Next authentication method: publickey
debug1: Offering public key: /home/sam/.ssh/id_rsa
debug1: Authentications that can continue: publickey,gssapi-keyex,gssapi-with-mic,password
debug1: Trying private key: /home/sam/.ssh/id_dsa
debug1: Next authentication method: password
sam@plum's password:
```

## Debug the server
You can debug from the server side by giving the command `/usr/bin/sshd -de` while working with root privileges. The server will run in the foreground, and its display might help you solve the problem.

# LPI TUNNELING/PORT FORWARDING
The `ssh` utility can forward a port (*port forwarding*; page 1266) through the encrypted connection it establishes. Because the data sent across the forwarded port uses the encrypted `ssh` connection as its data link layer (page 291), the term *tunneling* (page 1278) is applied to this type of connection: “The connection is tunneled through `ssh`.” You can secure protocols—including POP, X, IMAP, VNC, and WWW—by tunneling them through `ssh`.

# FORWARDING X11
The `ssh` utility makes it easy to tunnel the X11 protocol. For X11 tunneling to work, you must enable it on both the server and the client, and the client must be running the X Window System.

### SERVER
On the `ssh` server, enable X11 forwarding by setting the `X11Forwarding` declaration (page 706) to yes (the default) in the `/etc/ssh/sshd_config` file.

### TRUSTED CLIENT
On a client, enable trusted X11 forwarding by setting the `ForwardX11` (default is no; page 698) and `ForwardX11Trusted` (default is no, but set to yes as installed; page 698) declarations to yes in the `/etc/ssh/ssh_config` or `~/.ssh/config` file. Alternatively, you can specify the `-Y` option (page 695) on the command line to start the client in trusted mode.

When you enable X11 forwarding on a client, the client connects as a trusted client, which means the client trusts the server and is given full access to the X11 display. With full access to the X11 display, in some situations a client might be able to modify other clients of the X11 display. Make a trusted connection only when you trust the remote system. (You do not want someone tampering with your client.) If this concept is confusing, see the tip “The roles of X client and server might be counterintuitive” on page 459.

### NONTRUSTED CLIENT
On a client, enable nontrusted X11 forwarding by setting the `ForwardX11` (default is no; page 698) declaration to yes and the `ForwardX11Trusted` (default is no, but set to yes as installed; page 698) declaration to no in the `/etc/ssh/ssh_config` or `~/.ssh/config` file. Alternately, you can specify the `-X` option (page 695) on the command line to start the client in nontrusted mode.

A nontrusted client is given limited access to the X11 display and cannot modify other clients of the X11 display. Few clients work properly when they are run in nontrusted mode. If you are running an X11 client in nontrusted mode and encounter problems, try running in trusted mode (assuming you trust the remote system). Fedora/RHEL sets up `ssh` clients to run in trusted mode.

### RUNNING ssh
With X11 forwarding turned on, `ssh` tunnels the X11 protocol, setting the `DISPLAY` environment variable on the system it connects to and forwarding the required port. Typically you will be running from a GUI, which usually means that you are using `ssh` in a terminal emulator window to connect to a remote system. When you give an X11 command from an `ssh` prompt, OpenSSH creates a new secure channel that carries the X11 data, and the graphical output from the X11 program appears on the screen. Typically you will need to start the client in trusted mode.

```
[sam@guava ~]$ ssh plum
[sam@plum ~]$ echo $DISPLAY
localhost:10.0
```

By default, `ssh` uses X Window System display numbers 10 and higher (port numbers 6010 and higher) for forwarded X sessions. After you connect to a remote system using `ssh`, you can give a command to run an X application. The application will then run on the remote system with its display appearing on the local system, such that it appears to run locally.

# PORT FORWARDING
You can forward arbitrary ports using the **-L** and **-R** options. The **-L** option forwards a local port to a remote system, so a program that tries to connect to the forwarded port on the local system transparently connects to the remote system. The **-R** option does the reverse: It forwards remote ports to the local system. The **-N** option, which prevents `ssh` from executing remote commands, is generally used with **-L** and **-R**. When you specify **-N**, `ssh` works only as a private network to forward ports. An `ssh` command line using the **-L** or **-R** option has the following format:

```
$ ssh -N -L,|-R local-port:remote-host:remote-port target
```

where *local-port* is the number of the local port that is being forwarded to or from *remote-host*, *remote-host* is the name or IP address of the system that *local-port* gets forwarded to or from, *remote-port* is the number of the port on *remote-host* that is being forwarded from or to the local system, and *target* is the name or IP address of the system `ssh` connects to.

As an example, assume there is a POP mail client on the local system and that the POP server is on a remote network, on a system named **pophost**. POP is not a secure protocol; passwords are sent in cleartext each time the client connects to the server. You can make it more secure by tunneling POP through `ssh` (POP-3 connects on port 110; port 1550 is an arbitrary port on the local system):

```
$ ssh -N -L 1550:pophost:110 pophost
```

After giving the preceding command, you can point the POP client at **localhost:1550**. The connection between the client and the server will then be encrypted. (When you set up an account on the POP client, specify the location of the server as **localhost, port 1550**; details vary with different mail clients.)

# FIREWALLS
In the preceding example, *remote-host* and *target* were the same system. However, the system specified for port forwarding (*remote-host*) does not have to be the same as the destination of the `ssh` connection (*target*). As an example, assume the POP server is behind a firewall and you cannot connect to it via `ssh`. If you can connect to the firewall via the Internet using `ssh`, you can encrypt the part of the connection over the Internet:

```
$ ssh -N -L 1550:pophost:110 firewall
```

Here *remote-host* (the system receiving the port forwarding) is **pophost**, and *target* (the system that `ssh` connects to) is **firewall**.

You can also use `ssh` when you are behind a firewall (that is running `sshd`) and want to forward a port into your system without modifying the firewall settings:

```
$ ssh -R 1678:localhost:80 firewall
```

The preceding command forwards connections from the outside to port 1678 on the firewall to the local Web server. Forwarding connections in this manner allows you to use a Web browser to connect to port 1678 on the firewall when you connect to the Web server on the local system. This setup would be useful if you ran a Webmail program (page 758) on the local system because it would allow you to check your mail from anywhere using an Internet connection.

# COMPRESSION
Compression, which is enabled with the `-C` option, can speed up communication over a low-bandwidth connection. This option is commonly used with port forwarding. Compression can increase latency to an extent that might not be desirable for an X session forwarded over a high-bandwidth connection.

# CHAPTER SUMMARY
OpenSSH is a suite of secure network connectivity tools that encrypts all traffic, including passwords, thereby helping to thwart malicious users who might otherwise eavesdrop, hijack connections, and steal passwords. The `sshd` server daemon accepts connections from clients including `ssh` (runs a command or log in on another system), `scp` (copies files to and from another system), and `sftp` (securely replaces `ftp`). Helper programs including `ssh-keygen` (creates, manages, and converts authentication keys), `ssh-agent` (manages keys during a session), and `ssh-add` (works with `ssh-agent`) create and manage authentication keys.

To ensure secure communications, when an OpenSSH client opens a connection, it verifies that it is connected to the correct server. Then OpenSSH encrypts communication between the systems. Finally, OpenSSH makes sure the user is authorized to log in on or copy files to and from the server. You can secure many protocols—including POP, X, IMAP, VNC, and WWW—by tunneling them through `ssh`.

When it is properly set up, OpenSSH also enables secure X11 forwarding. With this feature, you can run securely a graphical program on a remote system and have the display appear on the local system.

# EXERCISES
- What is the difference between the `scp` and `sftp` utilities?
- How can you use `ssh` to find out who is logged in on a remote system?
- How would you use `scp` to copy your `~/.bashrc` file from the system named `plum` to the local system?
- How would you use `ssh` to run `xterm` on `plum` and show the display on the local system?
