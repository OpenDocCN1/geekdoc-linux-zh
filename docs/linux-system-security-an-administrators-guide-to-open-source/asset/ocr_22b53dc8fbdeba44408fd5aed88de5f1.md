by Whitfield Diffie and Martin Hellman in 1976. In 1977, Ron Rivest, Adi Shamir, and Len Adleman developed a similar algorithm called RSA.

Generally, asymmetric encryption algorithms can perform general data encryption (confidentiality) and can be used to generate digital signatures (authentication). It turns out that asymmetric algorithms are poor performers relative to symmetric algorithms. Consequently, asymmetric algorithms are most commonly used to encrypt secret keys for transmission over insecure channels and to generate digital signatures.

# # Hash Functions and Digital Signatures

# ## One-Way Cryptographic Hash Functions

A hash function (also known as a message digest), as it generally relates to computer science, is a mathematical function that takes data as input and produces a storage address as output. The output of any hash function is simply called the hash. A cryptographic one-way hash function, or simply a one-way hash function, is a mathematical transformation having the following properties:

+   - It accepts variable sized data and produces a value that is fixed in size (e.g., 160 bits).
+   - Computation of the hash from the data is easy.
+   - It is computationally impractical to compute the original data given the hash.
+   - It is computationally unfeasible to find two similar data sets that when transformed by the function, result in the same hash (this is called collision resistance).

The whole idea behind this type of algorithm is to come up with an identifier for any given file or message that will change if someone changes the file. In this way we can use these functions to fingerprint files.

Unfortunately, since most such hash algorithms are readily available, it is possible that someone could change both the file and the hash, making it impossible to detect the change. There are a number of ways to combat this potential vulnerability. One way is to compute the hash on important files in their pristine state and store them offline. Such is the approach of Tripwire (discussed in Chapter 14) and tiger (Chapter 13). Another method is to compute, then encrypt the hash. For example, include the hash in a digital signature (see Digital Signatures on page 45). This can also be done with RPM (see RPM Resources on page 28).

One purpose of such functions is to verify the integrity of data. We explore the application of hashing for integrity purposes in our discussions of tiger and Tripwire. Another purpose of hashing is for authentication. We examine this purpose in our discussions of pluggable authentication modules (PAM—see Chapter 5) and one-time passwords (OTP—see Chapter 6).