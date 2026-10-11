The Linux version of SSH is freely available and it includes both client and server software. There are also several excellent PC-based client implementations of SSH that are available free of charge.

# **How SSH Works**

Consider an example where a client is attempting to access a Linux server via SSH. Both the SSH daemon running on the Linux server and the SSH client have a pre-computed public/private key pair that makes up their SSH "identity." Here are the basic connection steps:

+   1. The client binds to a high local port and connects to port 22 on the server.

+   2. The client and server agree on the SSH version to use. This is necessary because v.1 and v.2 are not compatible.

+   3. The client requests the server's public key and host key.

+   4. The client and server agree on the encryption algorithm to use such as 3DES or IDEA.

+   5. The client generates a session key and encrypts it using the server's public key.

+   6. The server decrypts the session key, re-encrypts it with client's public key, and sends it back to client for verification.

+   7. The user authenticates to the server inside a data stream encrypted with the session key.

At this point, the connection has been established, and the client may proceed to interactively work on the server or to transfer files to or from it. Note that step 7 (client authentication) can be done in a number of ways (username/password, Kerberos, RSA, etc.). Chapter 13, "Strong User Authentication," discusses the topic of strong authentication in more depth.

There is a plethora of SSH implementations out there, but a GPL-protected open-source variant stands out among them: OpenSSH.

# **OpenSSH**

While the original implementation of SSH was freely available, starting with v.1.2.12, the licensing was made increasingly more restrictive until it eventually became a commercial product currently available from Data Fellows, Inc. The open-source community realized that the SSH concept was too valuable in the public domain and embarked on an organized effort to rewrite SSH into a free derivative. Starting in 1999, Björn Grönvall, and later the OpenBSD development team, took the original v.1.2.12 implementation and evolved it into what would be called *OpenSSH*. More than two years later, OpenSSH is now in version 2 and boasts support for an impressive array of platforms, including