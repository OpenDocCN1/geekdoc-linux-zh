# Encrypting and Signing Files with GnuPG

![](bbox=[0.25, 0.133, 0.84, 0.503])

Figure 2-2: Alice can digitally sign her message so that Bob can tell it's really from her.

Here's Alice sends her private message to Bob with the assurance that Bob can really tell it's from her:

+   1. Alice uses software to compute the message digest of the message and then encrypts the digest, using her private key. This is her digital signature for the message.
2. Alice encrypts the message (again, using some convenient software and Bob's public key).
3. She sends both the encrypted message and the digital signature to Bob.
4. Bob decrypts the message using his private key.
5. Bob decrypts the digital signature using Alice's public key. This gives him the message digest.
6. Bob computes the message digest of the message and compares it with what he got by decrypting the digital signature.
7. If the two message digests match, Bob can be sure that the message really came from Alice.