The next messages originate with PAM (page 458) and indicate that the user is not known to the system:

```
# grep sshd /var/log/messages
grape sshd[pan_unix] [2817]: check pass; user unknown
grape sshd[pan_unix] [2817]: authentication failure; logname= uid=0
euid=0 tty=NODEVXs50 ruser= host=peach.sobel1.com
```

Debug the client If either in these files or do not help solve the problem, try connecting with the -v option (either ssh or scp—the results should be the same). OpenSSH displays a lot of messages and one of them may help you figure out what the problem is.

```
$ ssh -v grape
OpenSSH_5.2p1, OpenSSL 1.0.0-fips-beta4 10 Nov 2009
debug1: Reading configuration data /etc/ssh/ssh_config
debug1: Applying options for *
debug1: Connecting to grape [192.168.0.3] port 22.
debug1: Connection established.
debug1: identity file /home/sam/.ssh/identity type -1
debug1: identity file /home/sam/.ssh/id_rsa type 1
...
debug1: Host 'grape' is known and matches the RSA host key.
debug1: Found key in /home/sam/.ssh/known_hosts:2
debug1: ssh_rsa_verify: signature correct
...
debug1: Authentications that can continue: publickey,password,keyboard-interactive
debug1: Trying private key: /home/sam/.ssh/id_dsa
debug1: Next authentication method: keyboard-interactive
debug1: Authentications that can continue: publickey,password,keyboard-interactive
debug1: Next authentication method: password
sam@grape's password:
```

Debug the server You can debug from the server side by running sshd with the -de options. The server will run in the foreground and its display may help you solve the problem.

# TUNNELING/PORT FORWARDING

The ssh utility allows you to forward a port (*port forwarding*, page 1099) through the encrypted connection it establishes. Because the data sent across the forwarded port uses the encrypted ssh connection as its data link layer (page 365), the term tunneling (page 1112) is applied to this type of connection: “The connection is tunneled through ssh.” You can secure protocols—including POP, X, IMAP, and WWW—by tunneling them through ssh.

Forwarding X11 The ssh utility makes it easy to tunnel the X11 protocol. For X11 tunneling to work, you must enable it on both the server and the client. On the server, you enable X11 forwarding by setting the X11Forwarding declaration to yes in the /etc/ssh/sshd_config file (page 637).

Trusted clients In the past there was only one way for a client to enable X11 forwarding; today there are two ways. Previously, when you enabled X11 forwarding (by setting