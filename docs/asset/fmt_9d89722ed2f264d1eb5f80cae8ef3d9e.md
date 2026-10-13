
On the other hand, the following directive is critical if you want to set up passphrase-based private/public key authentication on the standard SSH version 2:

```
#PubkeyAuthentication yes
```

The following directive confirms the use of the `authorized_keys` file on the remote system to confirm public keys for authentication:

```
#AuthorizedKeysFile .ssh/authorized_keys
```

The two directives that follow are typically ignored:

```
#AuthorizedKeysCommand none
#AuthorizedKeysCommandRunAs nobody
```

The following Rhosts directive is generally not used, as it applies to SSH version 1, and the less-secure Remote Shell (RSH):

```
#RhostsRSAAuthentication no
```

While the following directive could support the use of the `/etc/hosts.equiv` file to limit hosts that connect, that's not normally encouraged. Nevertheless, it is one method for SSH host-based security, beyond what's possible with an alternative such as TCP wrappers discussed in Chapter 10.

```
#HostbasedAuthentication no
```

As described earlier, the `.ssh/known_hosts` file stores RSA keys from remote systems, and is read because of the following default:

```
#IgnoreUserKnownHosts no
```

The following directive may help administrators who are converting from RSH to SSH, as they use `.rhosts` and `.shosts` files. But as it's not used by default, the following option is sensible:

```
#IgnoreRhosts yes
```

For systems and users where private/public passphrases aren't used, password-based authentication is needed, as enabled by this default:

```
#PasswordAuthentication yes
```

In general, you should never permit empty passwords, due to the security risks:

```
#PermitEmptyPasswords no
```

Challenge-response authentication is normally associated with one-time passwords common with remote terminals. While it can also work with PAM, it is normally disabled on SSH:

```
ChallengeResponseAuthentication = no
```

If you do set up a Kerberos system for the local network, as discussed in Chapter 12, you could set up some of the following options. The first two are almost self-explanatory, as they can enable Kerberos verification of a user and set up alternative Kerberos or local password authentication.

```
#KerberosAuthentication no
#KerberosOrLocalPasswd yes
```

The next two options relate to Kerberos authentication tickets and associated Andrew File System (AFS) tokens:

```
#KerberosTicketCleanup yes
#KerberosGetAFSToken no
```

This is followed by a directive that supports authentication using the Generic Security Services Application Programming Interface (GSSAPI) for client/server authentication:

```
GSSAPIAuthentication = yes
```

The following directive destroys GSSAPI credentials upon logout.

```
GSSAPICleanupCredentials = yes
```

Normally, hostname checks are strict:

```
GSSAPIStrictAcceptorCheck = yes
```

But normally authentication doesn't rely on SSH keys, as described here:

```
GSSAPIKeyExchange = yes
```

Access to PAM modules is supported:

```
UsePAM yes
```

The following directives allow the client to set several environmental variables.

The details are normally trivial between two Red Hat Enterprise Linux systems:

```
AcceptEnv LANG LC_CTYPE LC_NUMERIC LC_TIME LC_COLLATE LC_MONETARY LC_MESSAGES
AcceptEnv LC_PAPER LC_NAME LC_ADDRESS LC_TELEPHONE LC_MEASUREMENT
AcceptEnv LC_IDENTIFICATION LC_ALL
AcceptEnv XMODIFIERS
```

With the following setting, the `ssh-agent` command can be used to forward private keys to other remote systems:

```
#AllowAgentForwarding yes
```

In a similar fashion, TCP communications can be forwarded over an SSH connection:

```
#AllowTCPForwarding yes
```

The `GatewayPorts` directive is normally disabled to keep remote hosts from connecting to forwarded ports:

```
#GatewayPorts no
```

The following directive is important for anyone who needs remote access to a GUI tool:

```
X11Forwarding yes
```
