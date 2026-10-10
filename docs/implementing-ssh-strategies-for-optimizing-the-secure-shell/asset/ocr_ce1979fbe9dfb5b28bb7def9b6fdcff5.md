Table 8.1 Protocols That SSH Can Replace for Stronger Security
| SSH UTILITY | PROTOCOL |
|---|---|
| SSH (Terminal Access) | RSH, Rlogin, Rexec |
| SFTP | FTP, SMB, NFS, RCP |
| SSH with Chat | IRC |
| SSH with Backups | Rsync |

# Terminal Access

One of the most basic uses of SSH that I have only implied thus far is SSH terminal access. One of the primary reasons to install SSH is to provide secure terminal access. In order to replace the dangerous Berkeley R-protocols such as RSH and Rlogin, SSH needs to be used. Furthermore, if other terminal emulators such as Telnet are used in addition to the Berkeley R-protocols, the level of security across a network environment will be greatly reduced. SSH not only provides the same level of access that RSH, Rlogin, and Telnet do, but it does so in a secure manner through two-factor authentication, advanced authorization, and strong encryption.

SSH is often deployed for its secure terminal access, aside from the other features such as port forwarding and SFTP discussed in the next section. When dealing with remote management issues across the Internet or even insecure internal networks, Telnet, RSH, rexec, and Rlogin can and will cripple an organization's security infrastructure by allowing any passive user from gaining access to sensitive information, such as usernames, passwords, directory structures, and so on.

For example, RSH, Rlogin, and Rexec are clear-text protocols that provide some type of remote terminal emulation or remote execution service. All three of these protocols can be sniffed with any traffic analyzer that can reveal authentication and authorization information to an unauthorized user. This can potentially allow unauthorized users to gain access to sensitive authentication information and either log in to systems and/or devices or execute remote commands in an unauthorized fashion.