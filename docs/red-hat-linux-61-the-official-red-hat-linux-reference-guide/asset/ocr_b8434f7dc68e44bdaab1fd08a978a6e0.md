# Chapter 1. SSH Protocol

# 18.3.1. Transport Layer

The primary role of the transport layer is to facilitate safe and secure communication between the two hosts at the time of after authentication. The transport layer accomplishes this by handling the encryption and decryption of data and providing integrity protection of data packets as they are sent and received. In addition, the transport layer provides compression, speeding the transfer of information.

Once an SSH client connects a server, key information is exchanged so that the two systems can correctly construct the transport layer. The following steps occur during this exchange:

+   - Keys are exchanged
- The public key encryption algorithm is determined
- The symmetric encryption algorithm is determined
- The message authentication algorithm is determined
- The hash algorithm to be used is determined

During the exchange, the server identifies itself to the client with a unique host key. If the client has never communicated with this particular server before, the server's key will be unknown to the client and will not connect. OpenSSH handles this problem by asking the server's host key after the user is notified and verifies the acceptance of the new host key. In subsequent connections, the server's host key is checked against the saved version on the client, providing confidence that the client is indeed communicating with the intended server. If, in the future, the host key no longer matches, the user must remove the client's saved version before a connection can occur.

![](bbox=[0.08, 0.45, 0.14, 0.48])

> It is possible for an attacker to masquerade as the SSH server during the initial contact since the local system does not know the difference between the intended server and a false one set up by an attacker. To help prevent this, verify the integrity of a new SSH server by contacting the server administrator before connecting for the first time or in the event of a host key mismatch.

SSH is designed to work with almost any kind of public key algorithm or encoding format. After an initial key exchange creates a hash value for exchanges and a shared secret value, the two systems immediately begin calculating new keys and algorithms to protect authentication and future data over the connection.

After a certain amount of data has been transmitted using a given key and algorithm (the exact amount depends on the SSH implementation), another key exchange occurs, which generates another set of hash values and a new shared secret value. Even if an attacker is able to determine the hash and shared secret value, this information would be useful only for a limited period of time.

# 18.3.2. Authentication

Once the transport layer has constructed a secure tunnel to pass information between the two systems, the server tells the client different authentication methods supported, such as using a private-encoded signature or typing a password. The client then tries to authenticate itself to the server using one of these methods.

SSH servers and clients can be configured to allow different types of authentication, giving each side the optimal amount of control. The server can decide which encryption methods it will support based on its security model, and the client can choose the order of authentication methods to attempt from among the available options. Thanks to the secure nature of the SSH transport layer, even seemingly insecure authentication methods, such as a host and password-based authentication, are safe to use.