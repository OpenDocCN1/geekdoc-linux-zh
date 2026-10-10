
SSH_HOME/.ssh/known_hosts file, and refuses to connect hosts whose host key has changed. This provides maximum protection against trojan horse attacks. However, it can be somewhat annoying if you don't have good /etc/ssh_known_hosts files installed and frequently connect new hosts. Basically this option forces the user to manually add any new hosts. Normally this option is disabled, and new hosts will automatically be added to the known hosts files. The host keys of known hosts will be verified automatically in either case. The argument must be "yes" or "no".

**User**
Specifies the user to log in as. This can be useful if you have a different user name in different machines. This saves the trouble of having to remember to give the user name on the command line.

**UserKnownHostsFile**
Specifies a file to use instead of SSH_HOME/.ssh/known_hosts.

**UseRsh**
Specifies that login/rsh should be used for this host. It is possible that the host does not at all support the ssh protocol. This causes ssh to immediately exec rsh. All other options (except HostName) are ignored if it has been specified. The argument must be "yes" or "no".

## ENVIRONMENT

ssh will normally set the following environment variables:

- **DISPLAY** The DISPLAY variable indicates the location of the X11 server. It is automatically set by ssh to point to a value of the form "hostname:n" where hostname indicates the host where the shell runs, and n is an integer >= 1. Ssh uses this special value to forward X11 connections over the secure channel. The user should normally not set DISPLAY explicitly, as that will render the X11 connection insecure (and will require the user to manually copy any required authorization cookies).

- **HOME** Set to the path of the user's home directory.

- **LOGNAME** Synonym for USER; set for compatibility with systems that use this variable.

- **MAIL** Set to point to the user's mailbox.

- **PATH** Set to the default PATH, as specified when compiling ssh or, on some systems, /etc/environment or /etc/default/login.

- **SSH_AUTHENTICATION_FD** This is set to an integer value if you are using the authentication agent and a connection to it has been forwarded. The value indicates a file descriptor number used for communicating with the agent. On some systems, SSH_AUTHENTICATION_SOCKET may be used instead to indicate the path of a unix domain socket used to communicate with the agent. (This method is less secure, and is only used on systems that don’t support the first method.)

- **SSH_CLIENT** Identifies the client end of the connection. The variable contains three space-separated values: client ip-address, client port number, and server port number.

- **SSH_TTY** This is set to the name of the tty (path to the device) associated with the current shell or command. If the current session has no tty, this variable is not set.

- **TZ** The timezone variable is set to indicate the present timezone if it was set when the daemon was started (i.e., the daemon passes the value on to new connections).

- **USER** Set to the name of the user logging in.

Additionally, ssh reads /etc/environment and $HOME/.ssh/environment, and adds lines of the format VARNAME=value to the environment. Some systems may have still additional mechanisms for setting up the environment, such as /etc/default/login on Solaris.

## FILES

- `$HOME/.ssh/known_hosts` Records host keys for all hosts the user has logged into (that are not in /etc/ssh/ssh_known_hosts). See sshd manual page.

- `$HOME/.ssh/random_seed` Used for seeding the random number generator. This file contains sensitive data and should be read/write for the user and not accessible for others. This file is created the first time the program is run and updated automatically. The user should never need to read or modify this file.

- `$HOME/.ssh/identity` Contains the RSA authentication identity of the user. This file contains sensitive data and should be readable by the user but not accessible by others. It is possible to specify a passphrase when generating the key; the passphrase will be used to encrypt the sensitive part of this file under **IDEA**.

- `$HOME/.ssh/identity.pub` Contains the public key for authentication (public part of the identity file in human-readable form). The contents of this file should be added to `$HOME/.ssh/authorized_keys` on all machines where you wish to log in using RSA authentication. This file is not sensitive and can (but need not) be readable by anyone. This file is never used automatically and is not necessary; it is only provided for the convenience of the user.

- `$HOME/.ssh/config` This is the per-user configuration file. The format of this file is described above. This file is used by the `ssh` client. This file does not usually contain any sensitive information, but the recommended permissions are read/write for the user, and not accessible by others.

- `$HOME/.ssh/authorized_keys` Lists the RSA keys that can be used for logging in as this user. The format of this file is described in the `sshd` manual page. In the simplest form the format is the same as the .pub identity files (that is, each line contains the number of bits in n modulus, public exponent, modulus, and comment fields, separated by spaces). This file is not highly sensitive, but the recommended permissions are read/write for the user, and not accessible by others.

- `/etc/ssh_known_hosts` Systemwide list of known host keys. This file should be prepared by the system administrator to contain the public host keys of all machines in the organization. This file should be world-readable. This file contains public keys, one per line, in the following format (fields separated by spaces): system name, number of bits in n modulus, public exponent, modulus, and optional comment field. When different names are used for the same machine, all such names should be listed, separated by commas. The format is described on the `sshd` manual page.

The canonical system name (as returned by name servers) is used by `sshd` to verify the client host when logging in; other names are needed because `ssh` does not convert the user-supplied name to a canonical name before checking the key because someone with access to the name servers would then be able to fool host authentication.

- `/etc/ssh/ssh_config` Systemwide configuration file. This file provides defaults for those values that are not specified in the user's configuration file, and for those users who do not have a configuration file. This file must be world-readable.

- `$HOME/.rhosts` This file is used in .rhosts authentication to list the host/user pairs that are permitted to log in. (Note that this file is also used by rlogin and rsh, which makes using this file insecure.) Each line of the file contains a host name (in the canonical form returned by name servers), and then a user name on that host, separated by a space. This file must be owned by the user, and must not have write permissions for anyone else. The recommended permission is read/write for the user, and not accessible by others.

Note that by default sshd will be installed so that it requires successful RSA host authentication before permitting .rhosts authentication. If your server machine does not have the client's host key in /etc/ssh/known_hosts, you can store it in $HOME/.ssh/known_hosts. The easiest way to do this is to connect back to the client from the server machine using ssh; this will automatically add the host key in $HOME/.ssh/known_hosts.

- `$HOME/.shosts` This file is used exactly the same way as .rhosts. The purpose of having this file is to be able to use rhosts authentication with ssh without permitting login with rlogin or rsh.

- `/etc/hosts.equiv` This file is used during .rhosts authentication. It contains canonical hosts names, one per line (the full format is described on the sseq manual page). If the client host is found in this file, login is automatically permitted provided client and server user names are the same. Additionally, successful RSA host authentication is normally required. This file should only be writable by root.

- `/etc/.shosts.equiv` This file is processed exactly as /etc/hosts.equiv. This file may be useful to permit logins using ssh but not using rsh/rlogin.
