+   2. The server sends the client the server’s digital certificate containing the public key and a list of supported ciphers and key sizes in priority sequence.
+   3. The client compares the certification authority (CA) that issued the certificate to a list of trusted CAs and verifies that the certificate hasn’t expired.
+   4. The client generates a secret symmetric key based on the list of ciphers and then encrypts the key with the server’s public key and sends it to the server.
+   5. The server then decrypts the new symmetric session key using its own asymmetric private key.
+   6. After the symmetric key has been identified, both the server and client use that key along with the negotiated algorithm to secure all further communication.

# ## Message Digest Security

Another important aspect of securing data transmitted across the Internet is ensuring that data hasn’t been tampered with or changed since it left the sender. Data transmissions can be secured against tampering by using a hashing algorithm to create a fixed-length message called a message digest, as shown in Figure 11–23.

![](bbox=[0.1, 0.35, 0.75, 0.68])

**Figure 11-23 Creating a message digest**

The message digest is signed with the user’s private key and added to the end of the message transmission. The receiver opens the transmission and uses the sender’s public key with the hash algorithm to compute a message digest from the original message. If the message digests match, the receiver knows that no bits in the message have changed since the sender signed it. Two major hashing algorithms are in use in message digests today. Secure Hash Algorithm 1 (SHA-1), developed by the National Security Agency (NSA), produces 160-bit message digests and is considered the most secure. Message Digest 5 (MD5), developed by RSA Data Security, produces 128-bit digests and has been placed in the public domain. Because it requires no licensing, as of this writing MD5 is the most commonly used hashing algorithm, but cryptography experts fear it has flaws that could cause it to be broken in the future.