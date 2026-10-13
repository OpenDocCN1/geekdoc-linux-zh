configuration file. One typical option is in the current user's home directory, in the .gnupg/ subdirectory. Another typical option is in the /etc/gnupg directory.

# GPG2 Encryption Options

The development of a GPG2 key includes a choice of three different cryptographic algorithms. Each of these algorithms include a public and a private key. The public key can be distributed to others, for use in encrypting files and messages. The private key is used by the owner, and is the only way to decrypt the file or message.

+   - **RSA** Named for its developers, Rivest, Shamir, and Adelman. While typical RSA keys are 1024 or 2048 bits in length, they can be up to 4096 bits. Shorter keys of 512 bits have been cracked. It is in the public domain.
+   - **DSA** The Digital Signature Algorithm. Owned by the U.S. National Institute of Science and Technology, it has been made available for worldwide use, royalty-free. This is a U.S. Government standard that uses Secure Hash Algorithm (SHA) versions SHA-1 and SHA-2 as message digest hash functions. SHA-1 is being phased out; SHA-2 includes four hash functions with message digests of up to 512 bits, also known as SHA-512, the same hash as is now used for the RHEL 6 shadow password suite.
+   - **ElGamal** Developed by Taher Elgamal, this probabilistic encryption scheme predates the others. The choices for the number of bits for encryption keys range from 1024 to 3072 bits. While it was never patented, it may be covered under the patent for the Diffie-Hellman key exchange protocol.

# Generate a GPG2 Key

The `gpg2 --gen-key` command can be used to set up key pairs with one of four types of encryption schemes. Before running the command, be prepared with answers to the following questions:

+   - The number of bits for the encryption keys. Normally, the maximum number of bits is 4096, but an encryption key that complex may take a number of minutes to develop.
+   - The desired lifetime of the keys. Especially if you set up keys with a smaller number of bits, you should assume that a determined cracker would be able to decrypt the key within some number of months or weeks.