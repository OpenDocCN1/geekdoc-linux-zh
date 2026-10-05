# Chapter 12 Sendmail Security

The fact that authentication is used only for relaying reduces the overall security importance of the AUTH protocol. Readers familiar with encryption may have been hoping that AUTH was used to provide cryptographic authentication of both the source and content of e-mail messages. This is not really the case. AUTH is most effective as another tool in the fight against spam and unauthorized relaying.

RFC 2554 states that the AUTH extension can be optionally used to negotiate a security layer for subsequent protocol interaction, meaning message encryption. However, it is not really used in this way. STARTTLS is the protocol used to encrypt message transfers.

# Transport Layer Security

The AUTH extension uses a shared secret key. The authentication data is encrypted and decrypted with the same key, making AUTH a symmetric encryption system. TLS, on the other hand, is a public key encryption system. In fact, TLS is SSL, the public key encryption system used to secure Web communications. Securing e-mail with SSL requires the same information that is used to secure Web communications with SSL.

> NOTE To find out more about using SSL for a Linux web server, see Apache Web Server Administration by Charles Aul (SyAlex, 2000).

SSL public key cryptography requires three things:

+   A certificate authority Public key cryptography requires a trusted party called a certificate authority (CA). The CA is a server from which public keys are obtained. You cannot trust a public key that is obtained directly from the system, because unless you have the key you cannot authenticate that the system it claims to be. On the other hand, the CA is a well-known server. Some tools, such as the Netscape browser, come preconfigured to recognize any certificate authorities.

+   A certificate This is your public key. It is written in the form of an X.509 certificate, which contains your public key, the identity of your system, and dates that verify the key is currently valid. The X.509 certificate is signed by a CA. Thus, when you send your certificate to a remote server, the server can decrypt your certificate using the well-known public key of your CA to determine your identity.

+   A private key This is the key you use to encrypt your communications, which are then decrypted by the public key, or to decrypt communications that have been encrypted by the public key. The private key must be kept secure, but it cannot be stored in an encrypted format.