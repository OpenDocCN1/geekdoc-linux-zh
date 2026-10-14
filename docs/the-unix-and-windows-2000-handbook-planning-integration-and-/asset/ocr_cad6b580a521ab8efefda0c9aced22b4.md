# Figure 15.7
Using rdist to synchronize a remote directory structure to a local directory structure.

![](bbox=[0.24, 0.13, 0.92, 0.62])

to rdist is that it uses the rsh protocol and requires a client system trust relationship between the client and servers through the use of .rhosts files. While using .rhosts files is generally not a security issue, in some highly secure operations, .rhosts files may be discouraged because if mars.singlets.com allows rhost access from [jupiter.sniglets.com], a security breach on jupiter.sniglets.com now allows access to mars.sniglets.com.

> rdist—Designed to automatically replicate the directory structure from one system to another, without manual intervention.

| Table 15.4 Pros and Cons of Using rdist for Software Management |
| Pros | Cons |
| Highly Configurable | Requires machine-to-machine trust relationship |
| Provides for File Addition and Deletion | |
| Maintains Ownership and Creation Times | |
| No Clear Text Passwords | |