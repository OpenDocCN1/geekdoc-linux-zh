+   4. A Diffie-Hellman key agreement then follows, through which client and server agree on a secret session key, without having to send the key across the wire.
+   5. As with SSH1, communication is ultimately encrypted symmetrically.

The basic difference between SSH1 and SSH2 are mechanisms within the protocol that guarantee the integrity of the connection. A keyed-hash message authentication code (HMAC) is used for this purpose. The mechanism for the session key agreement (Diffie-Hellman) is different as well.

To see which SSH version an SSH server supports, you can log on to port 22 with Telnet. Table 5-2 shows the potential responses from the server:

| Protocol | Server Response |
|---|---|
| SSH1 only | SSH-1.5-OpenSSH... |
| SSH1 and SSH2 | SSH 1.99-OpenSSH... |
| SSH2 only | SSH-2.0-OpenSSH... |

**Table 5-2**

The following is an example of a Telnet connection on port 22:

```
da10:~ # telnet da20 22
Trying 10.0.0.20...
Connected to da20.
Escape character is '^]'.
SSH-1.99-OpenSSH_4.2
```

In the server configuration file /etc/ssh/sshd_config, the Protocol parameter defines which protocol versions are enabled.

For example, Protocol 2,1 in the configuration file means that SSH2 and SSH1 are both supported, but preference is given to SSH2. If SSH2 is not available, then SSH1 is used.

You can also specify the version to use when starting the clients (such as ssh -1 for SSH1).

# SSH Authentication Mechanism Configuration

The SSH server can decrypt the session key generated and encrypted by the client only if it also has the private key. If the server is unable to decrypt it, the communication ends at that point.

An absolute condition for the security of this procedure is that the client can check if the public host key of the server really belongs to the server.

SSH currently does not use any directory services (such as LDAP) or any certificates (such as with SSL) for public key management. This means that a random key pair can be easily created by anyone, even potential attackers, and included in the authentication dialog.

When first contacting an unknown server, it is possible to “learn” its host key. In this case, the SSH client then writes this key to the local key database.