key. On subsequent connections, the client compares the key provided by the server with the original key it stored. Although this test is not foolproof, the next one is quite secure.

The client then generates a random key, which it encrypts with both the server's public host key and the session key. The client sends this encrypted key to the server. The server, in turn, uses its private keys to decrypt the encrypted key. This process creates a key that is known only to the client and the server and is used to encrypt the rest of the session.

# FILES

OpenSSH clients and servers rely on many files. Global files are kept in /etc/ssh and user files in ~/.ssh. In this section, the first word in the description of each file indicates whether the client or the server uses the file.

**host authentication is a security risk**

> > Although OpenSSH can get authentication information from /etc/hosts, /etc/hosts.equiv, ~/.rhosts, and ~/.shosts, this chapter does not cover the use of these files because they are security risks. The default settings in the /etc/ssh/sshd_config configuration file prevent their use.

# /etc/ssh: GLOBAL FILES

Global files listed in this section appear in the /etc/ssh directory. They affect all users, but a user can override them with files in her ~/.ssh directory.

+   - **moduli**: client and server  Contains key exchange information that OpenSSH uses to establish a secure connection. Do not modify this file.
+   - **ssh_config**: client  The global OpenSSH configuration file (page 674). Entries here can be overridden by entries in a user's ~/.ssh/config file.
+   - **sshd_config**: server  The configuration file for sshd (page 679).
+   - **ssh_host_dsa_key**, **ssh_host_dsa_key.pub**: server  SSH protocol version 2 DSA host keys. Both files should be owned by root. The ssh_host_dsa_key.pub public file should be readable by anyone but writable only by its owner (644 permissions). The ssh_host_dsa_key private file should not be readable or writable by anyone except its owner (600 permissions).
+   - **ssh_host_rsa_key**, **ssh_host_rsa_key.pub**: server  SSH protocol version 2 RSA host keys. Both files should be owned by root. The ssh_host_rsa_key.pub public file should be readable by anyone but writable only by its owner (644 permissions). The ssh_host_rsa_key private file should not be readable or writable by anyone except its owner (600 permissions).
+   - **ssh_known_hosts**: client  Contains public RSA (by default) keys of hosts that users on the local system can connect to. This file contains information similar to that found in ~/.ssh/known_hosts, but is set up by the administrator and is available to all users.