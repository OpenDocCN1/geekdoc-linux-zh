### ~/.ssh/id_ed25519.pub
### ~/.ssh/id_rsa.pub
Contains the public key for authentication. These files are not sensitive and can (but need not) be readable by anyone.

### ~/.ssh/known_hosts
Contains a list of host keys for all hosts the user has logged into that are not already in the systemwide list of known host keys. See (8) for further details of the format of this file.

### ~/.ssh/rc
Commands in this file are executed by **ssh** when the user logs in, just before the user’s shell (or command) is started. See the (8) manual page for more information.

### /etc/hosts.equiv
This file is for host-based authentication (see above). It should only be writable by root.

### /etc/ssh/shosts.equiv
This file is used in exactly the sa way as hosts.equiv but allows host-based authentication without permitting login with rlogin/rsh.

### /etc/ssh/ssh_config
Systemwide configuration file. The file format and configuration options are described in ssh_config5.

+   * /etc/ssh/ssh_host_key
+   * /etc/ssh/ssh_host_dsa_key
+   * /etc/ssh/ssh_host_ecdsa_key
+   * /etc/ssh/ssh_host_ed25519_key
+   * /etc/ssh/ssh_host_rsa_key

These files contain the private parts of the host keys and are used for host-based authentication. If protocol version 1 is used, **ssh st** be setup root, since the host key is readable only by root. For protocol version 2, **ssh uses ssh-keysign8** to access the host keys, eliminating the requirement that **ssh** be setup root when host-based authentication is used. By default **ssh** is not setup root.

### /etc/ssh/ssh_known_hosts
Systemwide list of known host keys. This file should be prepared by the system administrator to contain the public host keys of all machines in the organization. It should be world-readable. See (8) for further details of the format of this file.

### /etc/ssh/sshrd
Commands in this file are executed by **ssh** when the user logs in, just before the user’s shell (or command) is started. See the (8) manual page for more information.