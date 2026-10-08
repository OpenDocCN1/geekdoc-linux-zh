# ssh 1321

-i identity_file

Select the file from which the identity (private key) for RSA authentication is read. Default is $HOME/.ssh/identity in the user's home directory. You can also specify identity files on a per-host basis in the configuration file. You can have multiple -i options and identities specified in configuration files.

-L login_name

Specify the user to log in as on the remote machine. You can also specify this option on a per-host basis in the configuration file.

-L port:host:hostport

Specify that the given port on the local (client) host is to be forwarded to the given host and port on the remote side. This option allocates a socket to listen to the port on the local side. Then, whenever a connection is made to this port, the connection is forwarded over the secure channel and a connection is made to host port hostport from the remote machine. You can also specify port forwarding in the configuration file. Only root can forward privileged ports. IPv6 addresses can be specified with an alternative syntax port/host.

-N

Redirect input from /dev/null (actually prevents reading from standard input). You must use this option when ssh runs in the background. A common trick is to use this option to run X11 programs on a remote machine. For example,

```
ssh -n shadows.cs.hut.fi emacs &
```

starts an editor on shadows.cs.hut.fi, and the X11 connection is automatically forwarded over an encrypted channel. The ssh program is put in the background. This option does not work if ssh needs to ask for a password or passphrase. Also see the -f option.

-N

Do not execute a command. This option is useful if you just want to forward ports (protocol version 2 only).

-o option

Specify the format used in the configuration file. This option is useful for specifying options for which there is no separate command-line option. The option has the same format as a line in the configuration file.

-p port

Specify the port to connect to the remote host. You can specify this option on a per-host basis in the configuration file.

-P

Use nonprivileged port for outgoing connections. You can use this option if your firewall does not permit connections from privileged ports. Note that this option turns off RhostsAuthentication and HostsRSAAuthentication.

-q

Suppress all warning and diagnostic messages. Display only fatal errors.