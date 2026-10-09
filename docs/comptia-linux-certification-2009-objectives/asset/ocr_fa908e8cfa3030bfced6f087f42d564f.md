only when the destination's private key is combined with the public key of the original server. While logging in to a remote system, the private and public keys are combined by the remote server for verification. The keys need to match if a user has to log in to the system and transfer files. Authenticity is established by the remote server, which then grants the necessary permissions.

# Key Files

The key pairs that you create using SSH are stored in different files depending on the algorithm you use.

| Files Created | Algorithm |
| --- | --- |
| id_dsa, id_dsa.pub | DSA |
| id_rsa, id_rsa.pub | RSA with SSH protocol version 2 |
| identity, identity.pub | RSA with SSH protocol version 1 |

# The /etc/ssh/sshd_config File

The /etc/ssh/sshd_config file is the SSH server configuration file. Most lines in this configuration file are commented, indicating the default settings that have been applied. You can remove the comment and change the default settings. A few SSH server configuration file options are listed in the following table.

| Use This sshd Option | If You Need To |
| --- | --- |
| X11Forwarding yes | Run or stop running a program on one system and display the X window output on another system. |
| X11Forwarding no | Stop running a program on one system and display the X window output on another system. |
| PermitRootLogin | Allow the root user to login via SSH. |
| MaxStartups Number | Specify the maximum number of connections that can be made to a host. |
| LoginGraceTime Time in seconds | Drop connections if the connection is not established within the login grace time. |
| AuthorizedKeysFile file name | Specify the location of the file that contains the authentication keys. |
| PermitEmptyPasswords yes/no | Specify whether a null password is allowed or denied. |