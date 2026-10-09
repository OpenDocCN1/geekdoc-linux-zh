
- `-t` (test) Checks the configuration file syntax and the sanity of the key files.
- `-D` (noDetach) Keeps sshd in the foreground. Useful for debugging; implied by -d.

## /etc/ssh/sshd_config CONFIGURATION FILE

The /etc/ssh/sshd_config configuration file contains one-line declarations. Each of these declarations starts with a keyword that is not case sensitive, followed by whitespace, followed by case-sensitive arguments. You must reload the sshd server before these changes will take effect.

### AllowUsers userlist

The userlist is a SPACE-separated list of usernames that specifies which users are allowed to log in using sshd. This list can include * and ? wildcards. You can specify a user as user or user@host. If you use the second format, make sure you specify the host as returned by hostname. Without this declaration, any user who can log in locally can log in using an OpenSSH client.

### ClientAliveCountMax n

The n specifies the number of client-alive messages that can be sent without receiving a response before sshd disconnects from the client. See ClientAliveInterval. The default is 3.

### ClientAliveInterval n

Sends a message through the encrypted channel after n seconds of not receiving a message from the client. See ClientAliveCountMax. The default is 0, meaning that no messages are sent.

This declaration passes messages over the encrypted channel (application layer; page 380) and is not susceptible to IP spoofing (page 1154). It differs from TCP-KeepAlive, which uses the TCP keepalive option (transport layer; page 380) and is susceptible to IP spoofing.

### DenyUsers userlist

The userlist is a SPACE-separated list of usernames that specifies users who are not allowed to log in using sshd. This list can include * and ? wildcards. You can specify a user as user or user@host. If you use the second format, make sure you specify the host as returned by hostname.

### HostbasedAuthentication yes | no

Tries rhosts and /etc/hosts.equiv authentication when set to yes. For a more secure system, set this declaration to no (default).

### IgnoreRhosts yes | no

Ignores .rhosts and .shosts files for authentication. Does not affect the use of /etc/hosts.equiv and /etc/ssh/shosts.equiv files for authentication. For a more secure system, set this declaration to yes (default).

### LoginGraceTime n

Waits n seconds for a user to log in on the server before disconnecting. A value of 0 means there is no time limit. The default is 120 seconds.

### LogLevel val

Specifies how detailed the log messages are. Choose val from QUIET, FATAL, ERROR, INFO (default), and VERBOSE.

### PasswordAuthentication

Permits a user to use a password for authentication. For a more secure system, set up automatic login (page 677) and set this declaration to **no**. The default is **yes**.

### PermitEmptyPasswords

Permits a user to log in on an account that has an empty password. The default is **no**.

### PermitRootLogin

Permits **root** to log in using an OpenSSH client. Given the number of brute-force attacks on a typical system connected to the Internet, it is important to set this declaration to **no**. (How you set this declaration is not an issue if the **root** account is locked.) The default is **yes**.

### Port num

Specifies that the sshd server listen on port num. It may improve security to change num to a nonstandard port. The default is port 22.

### StrictModes yes | no

Checks modes and ownership of the user’s home directory and files. Login fails for users other than the owner if the directories and/or files can be written to by anyone other than the owner. For a more secure system, set this declaration to **yes** (default).

### TCPKeepAlive yes | no

Periodically checks whether a connection is alive when set to **yes** (default). Checking causes the ssh or scp connection to be dropped when the client crashes or the connection dies for another reason, even if it is only temporary. This option tests the connection at the transport (TCP) layer (page 380). Setting this parameter to **no** causes the server not to check whether the connection is alive.

This declaration uses the TCP *keepalive* option, which is not encrypted and is susceptible to IP spoofing (page 1154). Refer to ClientAliveInterval (page 679) for a nonspoofable alternative.

### X11Forwarding yes | no

Allows X11 forwarding when set to **yes**. The default is **no**, but Ubuntu Linux sets X11Forwarding to **yes**. For trusted X11 forwarding to work, the ForwardX11 and the ForwardX11Trusted declarations must also be set to **yes** in either the ~/.ssh/config or /etc/ssh/ssh_config client configuration file (page 675). For more information refer to “Forwarding X11” on page 681.

## TROUBLESHOOTING

- **Log files**: There are several places to look for clues when you have a problem connecting with ssh or scp. First look for sshd entries in /var/log/ulog on the server. Following are messages you may see when you are using an AllowUsers declaration but have not included the user who is trying to log in (page 679). The messages that are marked (pam_unix) originate with PAM (page 478).

```
sudo grep sshd /var/log/auth.log
plum sshd[6927]: Invalid user sam from 192.168.0.12
plum sshd[6927]: Failed none for invalid user sam from 192.168.0.12 port 37134 ssh2
plum sshd[6927]: (pam_unix) check pass; user unknown
plum sshd[6927]: (pam_unix) authentication failure; logname= uid=0 euid=0 tty=ssh ruser=rhost=192.168.0.12
plum sshd[6927]: Failed password for invalid user sam from 192.168.0.12 port 37134 ssh2
```

- **Debug the client**: If entries in these files do not help solve the problem, try connecting with the -v option (either ssh or scp—the results should be the same). OpenSSH displays a lot of debugging messages, one of which may help you figure out what the problem is. You can use a maximum of three -v options to increase the number of messages that OpenSSH displays.

```
$ ssh -v plum
OpenSSH_5.3pl Debian-3ubuntu3, OpenSSH 0.9.8k 25 Mar 2009
debug1: Reading configuration data /etc/ssh/ssh_config
debug1: Applying options for "plum"
debug1: Connecting to plum [192.168.0.10] port 22.
debug1: Connection established.
debug1: identity file /home/sam/.ssh/identity type -1
debug1: identity file /home/sam/.ssh/id_rsa type 1
...
debug1: Host 'plum' is known and matches the RSA host key.
debug1: Found key in /home/sam/.ssh/known_hosts:1
debug1: ssh_rsa_verify: signature correct
debug1: Authentications that can continue: publickey,password
debug1: Next authentication method: publickey
debug1: Trying private key: /home/sam/.ssh/identity
debug1: Offering public key: /home/sam/.ssh/id_rsa
debug1: Authentications that can continue: publickey,password
debug1: Trying private key: /home/sam/.ssh/id_dsa
debug1: Next authentication method: password
sam@plum's password:
```

- **Debug the server**: You can debug from the server side by running sshd with the -de options. The server will run in the foreground and its display may help you solve the problem.

## TUNNELING/PORT FORWARDING

The ssh utility can forward a port (port forwarding; page 1165) through the encrypted connection it establishes. Because the data sent across the forwarded port uses the encrypted ssh connection as its data link layer (page 380), the term tunneling (page 1178) is applied to this type of connection: "The connection is tunneled through ssh." You can secure protocols—including POP, X, IMAP, VNC, and WWW—by tunneling them through ssh.

### Forwarding X11

The ssh utility makes it easy to tunnel the X11 protocol. For X11 tunneling to work, you must enable it on both the server and the client, and the client must be running the X Window System.

On the **ssh** server, enable X11 forwarding by setting the X11Forwarding declaration (page 680) to yes (the default) in the */etc/ssh/ssh_config* file.

On a client, enable trusted X11 forwarding by setting the ForwardX11 (default is **no**; see page 675) **and** ForwardX11Trusted (default is **no**, but set to **yes** as installed; see page 675) declarations to yes in the */etc/ssh/ssh_config* or *~/.ssh/ssh_config* file.

When you enable trusted X11 forwarding on a client, the client connects as a trusted client, which means that the client trusts the server and is given full access to the X11 display. With full access to the X11 display, in some situations a client may be able to modify other clients of the X11 display. Make a trusted connection only when you trust the remote system. (You do not want someone tampering with your client.) If this concept is confusing, see the tip “The roles of X client and server may be counterintuitive” on page 269.

An **ssh** client can connect to an **ssh** server as a trusted client or as a nontrusted client. A nontrusted client is given limited access to the X11 display and cannot modify other clients of the X11 display.

Few clients work properly when they are run in nontrusted mode. If you are running an X11 client in nontrusted mode and encounter problems, try running in trusted mode (assuming you trust the remote system). Ubuntu Linux sets up **ssh** clients to run in nontrusted mode by default.

When you start an **ssh** client, you can use the *-Y option* (page 672) on the command line to start the client in trusted mode. Alternatively, you can set the ForwardX11 **and** ForwardX11Trusted declarations to yes in a user’s *~/.ssh/config* configuration file (page 675) or, working with **root** privileges, in the global */etc/ssh/ssh_config* file (page 675) on the client to enable trusted X11 tunneling.

To use nontrusted tunneling, you can use the *-X option* (page 672) to set the ForwardX11 declaration to yes and set the ForwardX11Trusted declaration to no in one of the configuration files (page 675) on the server.

With trusted X11 forwarding turned on, **ssh** tunnels the X11 protocol, setting the DISPLAY environment variable on the system it connects to and forwarding the required port. Typically you will be running with a GUI, which usually means that you are using **ssh** on a terminal emulator to connect to a remote system. When you give an X11 command from an **ssh** prompt, OpenSSH creates a new secure channel that carries the X11 data and the graphical output from the X11 program appears on the screen. Typically you will need to start the client in trusted mode.

```
sam@dog:~$ ssh plum
sam@plum's password:
...
sam@plum:~$ echo $DISPLAY
localhost:10.0
```

By default, **ssh** uses X Window System display numbers 10 and higher (port numbers 6010 and higher) for forwarded X sessions. Once you connect to a remote system
