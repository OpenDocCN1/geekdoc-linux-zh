Table 2.9 (continued)

| OPTION | DESCRIPTION |
|---|---|
| LoginGraceTime | The amount of time, in seconds, the user has to complete the login process after initiating an authentication request. Values range from zero, no limit, to 600 seconds. |
| PermitEmptyPasswords | Allows (yes) or rejects (no) the ability for users to have empty passwords. In most situations, this should be no. |
| StrictModes | Enables (yes) or disables (no) the checking of a users' permission in their home directory and rhots files before accepting authentication. This should be set to yes to protect against world-writable files in home directories. |
| IdleTimeOut | The amount of time, in minutes, the session can remain unused before it is automatically closed. A setting of zero specifies no timeout, which may be ideal in certain backup processes. |

# User Public Key Authentication

The User Public Key Authentication section of the sshd_2_config file should look like the following:

```
```text
# HostKeyFile           hostkey
# PublicHostKeyFile     hostkey.pub
# RandomSeedFile        random_seed
# IdentityFile          identification
# AuthorizationFile     authorization
# AllowAgentForwarding  yes
```
```

Table 2.10 describes the User Public Key options available for the SSH server.