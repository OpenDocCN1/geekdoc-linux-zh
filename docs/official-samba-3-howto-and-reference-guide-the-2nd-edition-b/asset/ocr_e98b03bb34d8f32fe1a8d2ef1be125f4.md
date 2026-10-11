the above line would cause **nmbd** to request the master browser on on the specified subnets or addresses to synchronize their browse lists with the local server.

The IP addresses you choose would normally be the broadcast addresses of the remote networks, but can also be the IP addresses of known browse masters if your network config is that stable. If a machine IP address is given Samba makes NO attempt to validate that the remote machine is available, is listening, nor that it is in fact the browse master on its segment.

# **restrict anonymous (G)** Default: *restrict anonymous = 0*

The setting of this parameter determines whether user and group list information is returned for an anonymous connection. and mirrors the effects of the

```
HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\
Control\LSA\RestrictAnonymous
```

registry key in Windows 2000 and Windows NT. When set to 0, user and group list information is returned to anyone who asks. When set to 1, only an authenticated user can retrieve user and group list information. For the value 2, supported by Windows 2000/XP and Samba, no anonymous connections are allowed at all. This can break third party and Microsoft applications which expect to be allowed to perform operations anonymously.

The security advantage of using restrict anonymous = 1 is dubious, as user and group list information can be obtained using other means.

![](bbox=[0.15, 0.64, 0.85, 0.76])

**root** This parameter is a synonym for *root directory*.

**root dir** This parameter is a synonym for *root directory*.

# **root directory (G)** Default: *root directory = /homes/smb*

Example: *root directory = /homes/smb*

The server will **chroot()** (i.e. Change its root directory) to this directory on startup. This is not strictly necessary for secure operation. Even without it the server will deny access to files not in one of the service entries. It may also check for, and deny access to,