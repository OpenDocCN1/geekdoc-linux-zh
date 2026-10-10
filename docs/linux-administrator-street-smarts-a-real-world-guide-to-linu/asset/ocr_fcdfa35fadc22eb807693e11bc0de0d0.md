TABLE 6.1 Common SSH Server Configuration Options (continued)
| Keyword | Argument Type | Description |
| :--- | :--- | :--- |
| RsaAuthentication | Boolean | If this option is set to yes (the default), the server accepts Rivest/Shamir/Adleman (RSA) authentication for protocol level 1 sessions. This approach can improve security or eliminate the need to type a password, depending on how it's used. |
| PubKeyAuthentication | Boolean | If this option is set to yes (the default), the server accepts public key authentication for protocol level 2 sessions. This approach can improve security or eliminate the need to type a password, depending on how it's used. |
| AuthorizedKeysFile | Filename | Name of the file in which clients' keys for public key authentication are stored. |
| KerberosAuthentication | Boolean | If set to yes, this option enables SSH to accept Kerberos tickets and to authenticate users via a Kerberos server. This option is useful if your network uses Kerberos but is set to no by default. Additional options that begin with Kerberos can fine-tune the configuration; consult the sshd_config man page for details. |
| X11Forwarding | Boolean | If set to yes, this option enables the server to forward X session data. The default value is no. |
| Compression | Boolean | If this option is set to yes (the default), the server accepts requests from the client to enable compression. This option consumes CPU time but reduces network bandwidth use. |

Some configurations automatically add previously unknown sites to the key file, so you may not have to authorize a connection. Either way, subsequent connections to the same system will lack the prompt and need to type yes to authorize a connection. You will have to type a password, though, unless you modify the configuration as described shortly. (The password doesn't echo to the screen.)

Linux's ssh client passes the current username as part of the connection protocol. If your username on the server system is different from your username on the client system, you must