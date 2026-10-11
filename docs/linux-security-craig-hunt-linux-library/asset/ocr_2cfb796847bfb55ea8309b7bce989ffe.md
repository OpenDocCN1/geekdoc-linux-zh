```
unix 0 [ ACC ] STREAM LISTENING 491 /dev/log
unix 1 [ ] STREAM CONNECTED 985 @0000003d
unix 1 [ ] STREAM CONNECTED 886 @00000039
unix 1 [ ] STREAM CONNECTED 959 @0000003c
unix 1 [ ] STREAM CONNECTED 554 @00000021
unix 1 [ ] STREAM CONNECTED 740 @00000035
unix 0 [ ] STREAM CONNECTED 117 @00000013
unix 1 [ ] STREAM CONNECTED 744 @00000036
unix 1 [ ] STREAM CONNECTED 986 /dev/log
unix 1 [ ] STREAM CONNECTED 960 /dev/log
unix 1 [ ] STREAM CONNECTED 887 /dev/log
unix 1 [ ] STREAM CONNECTED 745 /dev/log
unix 1 [ ] STREAM CONNECTED 741 /dev/log
unix 1 [ ] STREAM CONNECTED 588 /dev/log
```

Chapter 5 contains a more detailed look into the tools available for monitoring your Linux server for this type of intrusion.

# Cryptanalysis and Brute Force Attacks

Most of the cryptographic algorithms in use today have proven to be robust enough to provide an appropriate level of confidentiality, integrity, and authentication. However, there have been several cases where some of these algorithms have been found to be vulnerable to attacks or mathematical exploits where the keyspace (the average number of combinations before the algorithm can be cracked) has been proven to be much smaller than initially thought. (By "mathematical exploits" I mean exploits that take advantage of flaws present in the functions used by the algorithm designers to derive prime numbers, generate keys, add entropy, and so on.)

In 1998 we saw a highly publicized case of cryptanalysis, where renowned security experts Bruce Schneier and "Mudge" discovered a number of security flaws in Microsoft's authentication algorithm for PPTP, a VPN protocol used in the Windows operating system. The MS-CHAP v.1 authentication algorithm was found to be vulnerable to password eavesdropping. In addition, the Microsoft Point-to-Point Encryption Algorithm (MPE) was also found to be much less effective than the 128-bit key strength that the vendor advertised, thereby exposing the user to eavesdropping attacks on the transmitted data. In 1999, Microsoft released MS-CHAP v.2 as an enhancement of the original version. However, a fundamental flaw still remains; the confidentiality of the VPN transmission is only as strong as the password that users choose for authentication.