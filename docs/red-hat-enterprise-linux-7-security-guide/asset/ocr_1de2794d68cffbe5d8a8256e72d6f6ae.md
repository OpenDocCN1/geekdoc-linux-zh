it can be instructed to generate DSA or ECDSA keys as well. The ECDSA (Elliptic Curve Digital Signature Algorithm) offers better performance at the same equivalent symmetric key length. It also generates shorter keys.

# Non-Default Port

By default, the `sshd` daemon listens on TCP port **22**. Changing the port reduces the exposure of the system to attacks based on automated network scanning, thus increasing security through obscurity. The port can be specified using the `Port` directive in the `/etc/ssh/sshd_config` configuration file. Note also that the default SELinux policy must be changed to allow for the use of a non-default port. You can do this by modifying the `ssh_port_t` SELinux type by typing the following command as `root`:

```
~~~bash
# semanage -a -t ssh_port_t -p tcp port_number
~~~
```

In the above command, replace *port_number* with the new port number specified using the `Port` directive.

# No Root Login

Provided that your particular use case does not require the possibility of logging in as the `root` user, you should consider setting the `PermitRootLogin` configuration directive to `no` in the `/etc/ssh/sshd_config` file. By disabling the possibility of logging in as the `root` user, the administrator can audit which user runs what privileged command after they log in as regular users and then gain root rights.

# Using the X Security extension

The X server in Red Hat Enterprise Linux 7 clients does not provide the X Security extension. Therefore clients cannot request another security layer when connecting to untrusted SSH servers with X11 forwarding. The most applications were not able to run with this extension enabled anyway. By default, the `ForwardX11Trusted` option in the `/etc/ssh/sshd_config` file is set to `yes`, and there is no difference between the `ssh -X remote_machine` (untrusted host) and `ssh -Y remote_machine` (trusted host) command.

> **WARNING**
> Red Hat recommends not using X11 forwarding while connecting to untrusted hosts.

# 4.3.12. Securing PostgreSQL

PostgreSQL is an Object-Relational database management system (DBMS). In Red Hat Enterprise Linux 7, the `postgresql-server` package provides PostgreSQL. If it is not installed, enter the following command as the root user to install it:

```
~~~bash
# yum install postgresql-server
~~~
```

Before you can start using PostgreSQL, you must initialize a database storage area on disk. This is called a database cluster. To initialize a database cluster, use the command `initdb`, which is installed with PostgreSQL. The desired file system location of your database cluster is indicated by the `-D` option. For example: