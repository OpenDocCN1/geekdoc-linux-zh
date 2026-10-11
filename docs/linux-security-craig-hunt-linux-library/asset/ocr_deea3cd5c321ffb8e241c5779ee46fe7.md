I recommend that you invoke `telnet` with the following options:

`telnet -a valid`

This command forces the remote user to provide proper Kerberos authentication before being handed over to the `login` program for interactive access.

**kshd** The `kshd` daemon is the Kerberized version of the `rshd` remote shell server that comes standard with Linux. Table 13.4 lists the options available when invoking the `kshd` command.

Table 13.4 Kerberos kshd Daemon Command-line Options

| Option | Meaning |
|---|---|
| -A | Don't allocate a reserved port for the stderr connection. |
| -C | Require clients to present a cryptographic checksum of initial connection information such as the name of the user that the client is trying to access in the initial authenticator. |
| -e | Require client to support encryption. |
| -M realm | Specify the Kerberos realm to use. (The default is the value of the default_realm variable in /etc/krb5.conf.) |

I recommend that you invoke `kshd` with the following options:

`kshd -e -c`

This command ensures the privacy of the connection by encrypting all the packets exchanged. In addition, the `-c` option prevents an attacker from changing the initial connection information.