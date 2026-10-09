```
sudo grep sshd /var/log/auth.logplum sshd[6927]: Invalid user sam from 192.168.0.12plum sshd[6927]: Failed none for invalid user sam from 192.168.0.12 port 37134 ssh2plum sshd[6927]: (pam_unix) check pass; user unknownplum sshd[6927]: (pam_unix) authentication failure; logname= uid=0 euid=0 tty=ssh ruser=rhost=192.168.0.12plum sshd[6927]: Failed password for invalid user sam from 192.168.0.12 port 37134 ssh2
```

Debug the client Of entries in these files do not help solve the problem, try connecting with the -v option (either ssh or scp—the results should be the same). OpenSSH displays a lot of debugging messages, one of which may help you figure out what the problem is. You can use a maximum of three -v options to increase the number of messages that OpenSSH displays.

```
$ ssh -v plumOpenSSH_5.3pl Debian-3ubuntu3, OpenSSH 0.9.8k 25 Mar 2009debug1: Reading configuration data /etc/ssh/ssh_configdebug1: Applying options for "debug1: Connecting to plum [192.168.0.10] port 22.debug1: Connection established.debug1: identity file /home/sam/.ssh/identity type -1debug1: identity file /home/sam/.ssh/id_rsa type 1...debug1: Host 'plum' is known and matches the RSA host key.debug1: Found key in /home/sam/.ssh/known_hosts:1debug1: ssh_rsa_verify: signature correctdebug1: Authentications that can continue: publickey,passworddebug1: Next authentication method: publickeydebug1: Trying private key: /home/sam/.ssh/identitydebug1: Offering public key: /home/sam/.ssh/id_rsadegub1: Authentications that can continue: publickey,passworddebug1: Trying private key: /home/sam/.ssh/id_dsadegubl: Next authentication method: passwordsam@plum's password:
```

Debug the server You can debug from the server side by running sshd with the -de options. The server will run in the foreground and its display may help you solve the problem.

# # TUNNELING/PORT FORWARDING

The ssh utility can forward a port (port forwarding; page 1165) through the encrypted connection it establishes. Because the data sent across the forwarded port uses the encrypted ssh connection as its data link layer (page 380), the term tunneling (page 1178) is applied to this type of connection: "The connection is tunneled through ssh." You can secure protocols—including POP, X, IMAP, VNC, and WWW—by tunneling them through ssh.

Forwarding X11 The ssh utility makes it easy to tunnel the X11 protocol. For X11 tunneling to work, you must enable it on both the server and the client, and the client must