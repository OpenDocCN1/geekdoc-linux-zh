**CROSS-REFERENCE:** Chapter 24 describes how to set up a MySQL database server.

# ## User services

Fedora and RHEL can provide end users with a variety of network services. These services let users run remote programs, send messages in real time, and get information on active users.

# ### Remote execution servers

Remote execution servers respond to requests from other computers to run commands on the local computer. This can be a security issue, so be careful in configuring these services. Three remote execution service daemons are available with Fedora and RHEL: Rsh, Rexec, and Kshell.

+   - The Rsh service (`/usr/sbin/in.rshd`) accepts requests for remote execution requests that were initiated by the `rsh` command (from other Linux or UNIX systems). By default, the service is off. The host or user (or both) must be allowed access before remote execution is permitted. Access is configured in the `/etc/hosts.equiv` file or in the `.rhosts` file in each user’s home directory.

+   - The Rexec service (`/usr/sbin/in.rexecd`) accepts remote execution requests from the `rexec` command (from other Linux or UNIX systems). By default, the service is off. To allow remote execution, the user making the request must provide a valid user name and password.

+   - The Kshell service (`/usr/kerberos/sbin/kshd`) receives remote execution requests from the `rsh` command. It uses Kerberos authentication and encryption, making it more secure than the alternative in.rshd daemon. By default, the service is off. However, if you turn it on (by editing the `/etc/xinetd.d/kshd` file and changing the `disable = yes` entry to `disable = no`), it takes precedence over the `in.rshd` daemon.

The OpenSSH service (using the sshd daemon) described earlier can also be used for remote execution. OpenSSH is a more secure way to do remote execution than the other methods just described. Therefore, in most cases you should bypass these services and use OpenSSH for remote execution.

**CROSS-REFERENCE:** Login commands for using login services are described in Chapter 16.

# ### Talk server

Use the `in.talk` or `in.ntalk` servers to allow users to communicate using the `talk` command. The `talk` command enables users to type messages back and forth in real time. The `talk` daemon handles requests on port 517, and the `ntalk` daemon handles requests on port 518.