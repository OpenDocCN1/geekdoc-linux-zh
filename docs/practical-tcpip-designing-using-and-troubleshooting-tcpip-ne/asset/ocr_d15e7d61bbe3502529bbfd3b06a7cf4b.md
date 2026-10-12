Multiple Phase 2 exchanges (i.e. conversations) can happen after a single Phase 1 exchange – because the channel set up in Phase 1 can be used repeatedly, reducing the overall amount of network traffic required.

In Phase 1, the two systems use the Diffie-Hellman key agreement method. This lets two parties converse over a public communications channel to negotiate a secret number, even if they don't have any shared secret information to begin with. Even though Eve the eavesdropper can listen in to the whole conversation, she won't be able to find out what the secret number is. (This sounds like magic but see the Notes for more information.) In IKE the two parties use the secret number they agreed as the encryption key for the rest of the IKE session.

IKE gets complicated because there are many different options in each phase. In Phase 1 the two parties can:

+   authenticate using a shared secret (almost like a password) that both of them know, or using digital certificates and signatures, or using public-key encryption. With shared secrets, you still have to distribute them manually, which still isn't scalable to large numbers of sites. With public-key encryption or certificates, if Alice and Dave want to set up a VPN, they look up each other's public encryption keys (e.g. from a Secure DNS server or in a public LDAP directory of public keys) and can then use IKE as before. There is no longer any need to distribute keys or secrets manually

+   use either main mode or aggressive mode to set up the secure channel. (Main mode hides the identities of the two parties from snoopers but aggressive mode uses fewer packets.)

+   use different encryption and authentication algorithms, and different groups (used in the secret-number generation process) for the Diffie-Hellman exchange. There are currently five of these groups (named “1” … “5”). They are also called Oakley groups as they were used in the earlier Oakley protocol. (In fact IKE is a mixture of Oakley and ISAKMP – the Internet Security Association and Key Management Protocol.)

In Phase 2, the parties can:

+   use different encryption and authentication algorithms

+   have perfect forward secrecy (PFS) or not

+   issue many proposals to one another, indicating which type of encryption algorithms each one is prepared to accept. The other party has to choose one of the proposals, and this specifies the details of the SA IKE will create. IPsec's ESP or AH then use this SA as before

+   specify the key lifetime, i.e. the duration after which new keys ought to be renegotiated.

IKE runs over UDP, and uses port 500.

In the next module, we show the VPN settings for a Windows client.