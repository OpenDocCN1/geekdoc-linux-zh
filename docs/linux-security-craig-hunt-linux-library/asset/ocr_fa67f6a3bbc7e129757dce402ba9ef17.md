Table 12.1 lists the most frequently used variables in the `sshd_config` file.

# **Table 12.1** `/etc/ssh/sshd_config` Variables

| Option | Meaning | Default |
| :--- | :--- | :--- |
| `AllowTcpForwarding` | Specifies whether TCP forwarding is permitted. | Yes |
| `AllowUsers user1 user2...` | Specifies users to allow SSH access (exclusively). | All users allowed |
| `DenyUsers user1 user2...` | Specifies users to ban from SSH access (exclusively). | No users banned |
| `Ciphers cipher1, cipher2...` | Specifies encryption cipher to be used (SSH v.2). | 3des-cbc, blowfish-cbc, arcfour, cast128-cbc |
| `DSAAuthentication` | Specifies whether DSA authentication is allowed (SSH v.2). | Allowed |
| `IgnoreRhosts` | Specifies whether .rhosts and .shosts should be ignored. | Yes |
| `KerberosAuthentication` | Specifies whether Kerberos authentication is allowed. | Yes |
| `PasswordAuthentication` | Specifies whether password authentication is allowed. | Yes |
| `PermitEmptyPasswords` | Specifies whether empty passwords should be allowed. | No |
| `PermitRootLogin` | Specifies whether root log-ins over SSH should be allowed. | Yes |