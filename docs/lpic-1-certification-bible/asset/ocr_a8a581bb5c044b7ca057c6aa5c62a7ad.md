# Table 17-5 (continued)

| Entry | Function | Default |
|---|---|---|
| KeepAlive <yes|no> | Sends keep-alive messages to the client. | Yes |
| KerberosAuthentication <yes|no> | Enables or disables Kerberos authentication. Kerberos is a very secure system designed for single login across many different hosts and services. | Yes |
| KerberosOrLocalPassword <yes|no> | If Kerberos authentication fails, uses the local password file. | Yes |
| KerberosTgtPassing <yes|no> | Specifies whether a Kerberos TGT may be forwarded to the server. | No |
| KerberosTicketCleanup <yes|no> | Specifies whether to automatically destroy the user's ticket cache file on logout. | Yes |
| KeyRegenerationInterval <n seconds> | Specifies how often to regenerate the SSH server key. | 3600 seconds. |
| ListenAddress <ip address> | Specifies which local addresses to listen on. | All addresses. |
| LoginGraceTime <n seconds> | If the user does not log in within the specified time, he or she is disconnected. | 600 Seconds. |
| LogLevel <QUIET, FATAL, ERROR, INFO, VERBOSE, DEBUG> | Sets the logging level. | INFO |
| MaxStartups <n> | The number of unauthenticated connections allowed at one time. | 10 |
| PasswordAuthentication <yes|no> | Enables or disables password authentication. | Yes |
| PermitEmptyPasswords <yes|no> | Specifies if the server will allow blank passwords. | No |
| PermitRootLogin <yes|no|without-password> | Enables or disables remote login of the root account. | Yes |
| PidFile <file name> | Specifies the file that holds the process ID information. | /var/run/ssh.pid |
| Port <n> | Specifies the port number that SSH listens on. | 22 |
| PrintMotd <yes|no> | Specifies whether or not to show the /etc/motd file when a user logs in. | Yes |