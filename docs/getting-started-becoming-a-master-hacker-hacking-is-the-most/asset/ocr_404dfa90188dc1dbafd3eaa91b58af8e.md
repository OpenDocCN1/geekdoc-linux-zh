very slow, about 1,000 times slower than symmetric cryptography, so we don't want to use it for bulk encryption or streaming communication. It does, however, solve the key exchange problem. Since we don't need to have the same key on both ends of a communication, we don't have the issue of key exchange.

Asymmetric cryptography is used primarily when we have two entities unknown to each other that want to exchange a **small** bit of information, such as a key or other identifying information, such as a certificate. It is not used for bulk or streaming encryption due to its speed limitations.

Some of common asymmetric encryption schemes you should be familiar with are:  **Diffie-Hellman** - Many people in the field of cryptography regard the Diffie-Hellman key exchange to be the greatest development in cryptography (I would have to agree). Without going deep into the mathematics, Diffie and Hellman developed a way to generate keys without having to exchange the keys, thereby solving the key exchange problem that plagues symmetric key encryption.

**RSA** - Rivest, Shamir, and Adleman is a scheme of asymmetric encryption that uses factorization of very large prime numbers as the relationship between the two keys.

**PKI** - Public key infrastructure is the widely used asymmetric system for exchanging confidential information using a private key and a public key.