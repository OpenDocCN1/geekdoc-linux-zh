# **Table 9.12 How ssh interacts and behaves (continued).**

| Option | Purpose | Values |
| :--- | :--- | :--- |
| IdleTimeout | Specifies how long to wait before breaking an idle connection. | A positive integer followed by **s** for seconds, **m** for minutes, **h** for hours, **d** for days, or **w** for weeks; the default is seconds. |
| KeepAlive | Tells the server to send messages to the client to ensure that the connection is still open and valid. It closes the connection if it cannot reach the client. | Either **yes** or **no** in both server and client configuration files; the default is **yes**. |
| KeyRegenerationInterval | Allows the server to automatically generate a new security key on a regular basis. This prevents keeping one in place long enough for someone to manage to decrypt it. | A positive integer; the default is every 3,600 seconds. Use 0 to shut off this feature. |
| ListenAddress | Identifies the interface that sshd is listening on. | IP address of interface |
| LoginGraceTime | Specifies how long the server waits before hanging up on a user who has not fully logged in for any reason. | A positive integer in seconds; the default is 600. Use 0 to shut off this feature. |
| Port | Sets a specific port for sshd to listen on. | Unique port not assigned to another process; the default is 22. |
| PrintMotd | Specifies whether to print the contents of /etc/motd when a connection is made, which the system would do during a **telnet** session or local login. | Either **yes** or **no**; the default is **yes**. |
| QuietMode | Specifies to use minimal logging. Only log fatal errors. | Either **yes** or **no**; the default is **no** because no logging means no security analysis. |
| ServerKeyBits | Specifies the number of bits used to generate the server security keys. | 512, 768, and 1,024 are the most common options; the default is 768. |

*(continued)*