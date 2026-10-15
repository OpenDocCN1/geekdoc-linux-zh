You can use *magic cookies* to breathe life into your displayed messages. Magic cookies are symbolic constants that are replaced by system information. Table 23.1 lists valid magic cookies for the message command and their representation.

| Cookie | Description |
|---|---|
| `%t` | Local time (form Thu Nov 15 17:12:42 1990) |
| `%F` | Free space in partition of CWD (kbytes) [Not supported on all systems] |
| `%C` | Current working directory |
| `%E` | The maintainer's email address as defined in `ftpaccess` |
| `%R` | Remote hostname |
| `%L` | Local hostname |
| `%u` | Username as determined via RFC931 authentication |
| `%U` | Username given at login time |
| `%m` | Maximum allowed number of users in this class |
| `%N` | Current number of users in this class |
| `%B` | Absolute limit on disk blocks allocated |
| `%b` | Preferred limit on disk blocks |
| `%Q` | Current block count |
| `%I` | Maximum number of allocated inodes (+1) |
| `%i` | Preferred inode limit |
| `%q` | Current number of allocated inodes |
| `%H` | Time limit for excessive disk use |
| `%h` | Time limit for excessive files |

**Ratios**

| Cookie | Description |
|---|---|
| `%xu` | Uploaded bytes |
| `%xd` | Downloaded bytes |
| `%XR` | Upload/Download ratio (1:n) |
| `%xC` | Credit bytes |
| `%xT` | Time limit (minutes) |
| `%XE` | Elapsed time since login (minutes) |
| `%xL` | Time left |
| `%xU` | Upload limit |
| `%xD` | Download limit |

To understand how this command works, imagine that you want to display a welcome message to everyone who logs in to the FTP server. An entry of

```
message /home/ftp/welcome.msg  login
message /welcome.msg        login
```