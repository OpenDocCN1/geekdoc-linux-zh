| ForwardX11 | yes | no |
| --- | --- | --- |
|  | When set to yes, automatically forwards X11 connections over a secure channel in non- trusted mode but does not set the DISPLAY shell variable. If ForwardX11Trusted is also set to yes, the connections are made in trusted mode. Alternatively, you can use -X on the command line to redirect X11 connections in untrusted mode. The default value for this parameter is no; set it to yes to enable X11 forwarding. For X11 forwarding to work, you must also set X11Forwarding to yes in the /etc/sshd_config file on the server (page 680). For more information refer to “Forwarding X11” on page 681. |  |

| ForwardX11Trusted | yes | no |
| --- | --- | --- |
|  | Works in conjunction with ForwardX11, which must be set to yes for this declaration to have any effect. When this declaration is set to yes (as it is on Ubuntu Linux systems) and ForwardX11 is set to yes, this declaration sets the DISPLAY shell variable and gives remote X11 clients full access to the original (server) X11 display. Alternatively, you can use -Y on the command line to redirect X11 connections in trusted mode. The default value for this declaration is no but Ubuntu Linux sets it to yes. For X11 forwarding to work, X11Forwarding must also be set to yes in the /etc/sshd_config file on the server (page 680). For more information refer to “Forwarding X11” on page 681. |  |

| HashKnownHosts | Causes OpenSSH to hash hostnames and addresses in the ~/.ssh/known_hosts file when set to yes. The hostnames and addresses are written in cleartext when it is set to no. Ubuntu Linux sets this declaration to yes to improve system security. See page 668 for more information on the known_hosts file. |  |  |
| --- | --- | --- | --- |

| Host hostnames | Specifies that the following declarations, until the next Host declaration, apply only to hosts that hostnames matches. The hostnames can include ? and * wildcards. A single * specifies all hosts. Without this keyword, all declarations apply to all hosts. |  |  |
| --- | --- | --- | --- |

| HostbasedAuthentication | yes | no |  |
| --- | --- | --- | --- |
|  | Tries rhosts authentication when set to yes. For a more secure system, set to no (default). |  |  |

| HostKeyAlgorithms algorithms | The algorithms is a comma-separated list of algorithms the client uses in order of preference. Choose algorithms from ssh-rsa or ssh-dss. The default is ssh-rsa,ssh-dss. |  |  |
| --- | --- | --- | --- |
| Port num | Causes OpenSSH to connect to the remote system on port num. The default is 22. |  |  |

| StrictHostKeyChecking | yes | no | ask |
| --- | --- | --- | --- |
|  | Determines whether and how OpenSSH adds host keys to a user’s known_hosts file. Set this option to ask to ask whether to add a host key when connecting to a new system, set it to no to add a host key automatically, and set it to yes to require that host keys be added manually. The yes and ask arguments cause OpenSSH to refuse to connect to a system whose host key has changed. For a more secure system, set this option to yes or ask. The default is ask. |  |  |

| TCPKeepAlive | yes | no |
| --- | --- | --- |
|  | Periodically checks whether a connection is alive when set to yes (default). Checking causes the ssh or scp connection to be dropped when the server crashes or the |  |