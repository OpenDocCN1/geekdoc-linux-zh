**Table 3-1 (continued)**

| Component | Description |
|---|---|
| /usr/bin/ssh-keygen | You use this program to generate the public and private key pairs you need for the public key cryptography used in OpenSSH. The ssh-keygen program can generate key pairs for both RSA and DSA (Digital Signature Algorithm) authentication. |
| /etc/ssh/sshd_config | This configuration file for the sshd server specifies many parameters for sshd — including the port to listen to, the protocol to use (there are two versions of SSH protocols, SSH1 and SSH2, both supported by OpenSSH), and the location of other files. |
| /etc/ssh/ssh_config | This is the configuration file for the ssh client. Each user can also have a ssh configuration file named config in the .ssh subdirectory of the user's home directory. |

OpenSSH uses public key encryption where the sender and receiver both have a pair of keys — a public key and a private key. The public keys are freely distributed, and each party knows the other's public key. The sender encrypts data by using the recipient's public key. Only the recipient's private key can then decrypt the data.

To use OpenSSH, do both of the following:

+   - If you want to support SSH-based remote logins on a host, start the sshd server on your system. Type `ps ax | grep sshd` to see if the server is already running. If not, log in as root, and type the following command at the shell prompt to ensure that the sshd server starts at system reboot: `chkconfig --level 35 sshd on` To start the sshd server immediately, type the following command: `service sshd start`
+   - Generate the host keys with the following command: `ssh-keygen -d -f /etc/ssh/ssh_host_key -N ''`

The -d flag causes the ssh-keygen program to generate DSA keys, which the SSH2 protocol uses. If you see a message saying that the file /etc/ssh/ssh_host_key already exists, that means that the key pairs were generated during Red Hat Linux installation. You can then use the existing file without having to regenerate the keys.