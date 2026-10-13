# The Secure Shell: OpenSSH

Although a firewall can protect a network from attempts to break into it from the outside, the problem of securing legitimate communications to the network from outside sources still exists. A particular problem is one of users who want to connect to your network remotely. Such connections could be monitored, and information such as passwords and user IDs used when the user logs into your network could be copied and used later to break in. One solution is to use SSH for remote logins and other kinds of remote connections such as FTP transfers. SSH encrypts any communications between the remote user and a system on your network.

Two different implementations of SSH currently use what are, in effect, two different and incompatible protocols. The first version of SSH, known as SSH1, uses the original SSH protocol. Version 2.0, known as SSH2, uses a completely rewritten version of the SSH protocol. Encryption is performed in different ways, encrypting different parts of a packet. SSH1 uses server and host keys to authenticate systems, whereas SSH2 uses only host keys. Furthermore, certain functions, such as sftp, are supported only by SSH2.

Note A commercial version of SSH is available from SSH Communications Security, whose Web site is www.ssh.com. SSH Communications Security provides SSH free for noncommercial use and sells SSH for commercial use through Datafellows.

The SSH protocol has become an official Internet Engineering Task Force (IETF) standard. A free and open source version is developed and maintained by the OpenSSH project, currently supported by the OpenBSD project. OpenSSH is the version supplied with most Linux distributions, including Red Hat, Mandrake, Caldera, SUSE, and Debian. You can find out more about OpenSSH at www.openssh.org, where you can download the most recent version, though your distribution will provide current RPM versions.

# SSH Encryption and Authentication

SSH secures connections by both authenticating users and encrypting their transmissions. The authentication process is handled with public key encryption (see Chapter 16). Once authenticated, transmissions are encrypted by a cipher agreed upon by the SSH server and client for use in a particular session. SSH supports multiple ciphers. Authentication is applied to both hosts and users. SSH first authenticates a particular host, verifying that it is a valid SSH host that can be securely communicated with. Then the user is authenticated, verifying that the user is who they say they are.

SSH uses strong encryption methods, and their export from the United States may be restricted. Currently, SSH can deal with the following kinds of attacks:

+   - IP spoofing, where a remote host sends out packets that pretend to come from another, trusted host
+   - IP source routing, where a host can pretend an IP packet comes from another, trusted host
+   - DNS spoofing, where an attacker forges name server records
+   - Interception of clear text passwords and other data by intermediate hosts
+   - Manipulation of data by people in control of intermediate hosts
+   - Attacks based on listening to X authentication data and spoofed connections to the X11 server

# Encryption

The public key encryption used in SSH authentication makes use of two keys: a public key and a private key. The public key is used to encrypt data, while the private key decrypts it. Each host or user has their own public and private keys. The public key is distributed to other hosts, who can then use it to encrypt authentication data that only the host's private key can decrypt. For example, when a host sends data to a user on another system, the host encrypts the authentication data with a public key, which it previously received from that user. The data can be decrypted only by the user's corresponding private key. The public key can safely be sent in the open from one host to another, allowing it to be installed safely on different hosts. You can think of the process as taking place between a client and a server. When the client sends data to the server, it first encrypts the data using the server's public key. The server can then decrypt the data using its own private key.