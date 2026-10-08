```
- [ Hash modes ] -
  #  Name                                                       | Category
============================================================================
  0  MD4                                                         | Raw Hash
  0  MD5                                                         | Raw Hash
  5100  Half MD5                                                | Raw Hash
  100  SHA1                                                      | Raw Hash
  1300  SHA2-224                                                | Raw Hash
  1400  SHA2-256                                                | Raw Hash
 10800  SHA2-384                                                | Raw Hash
 1700  SHA2-512                                                | Raw Hash
 17300  SHA3-224                                                | Raw Hash
 17400  SHA3-256                                                | Raw Hash
 17500  SHA3-384                                                | Raw Hash
 17600  SHA3-512                                                | Raw Hash
 17700  Keccak-224                                            | Raw Hash
 17800  Keccak-256                                            | Raw Hash
 17900  Keccak-384                                            | Raw Hash
 18000  Keccak-512                                            | Raw Hash
  600  BLAKE2b-512                                             | Raw Hash
 10100  Siphash                                               | Raw Hash
  6000  RIPEMD-160                                            | Raw Hash
  6100  whirlpool                                               | Raw Hash
  6900  GOST R 34.11-94                                       | Raw Hash
 11700  GOST R 34.11-2012 (Streebog) 256-bit, big-endian       | Raw Hash
 11800  GOST R 34.11-2012 (Streebog) 512-bit, big-endian       | Raw Hash
   10  md5($pass.$salt)                                       | Raw Hash, Salted and/or Iterated
   20  md5($salt.$pass)                                       | Raw Hash, Salted and/or Iterated
   30  md5(utf16le($pass).$salt)                              | Raw Hash, Salted and/or Iterated
   40  md5($salt.utf16le($pass))                              | Raw Hash, Salted and/or Iterated
 3800  md5($salt.$pass.$salt)                                 | Raw Hash, Salted and/or Iterated
 3710  md5($salt.md5($pass))                                   | Raw Hash, Salted and/or Iterated
 4010  md5($salt.md5($salt.$pass))                             | Raw Hash, Salted and/or Iterated
 4110  md5($salt.md5($pass.$salt))                             | Raw Hash, Salted and/or Iterated
 2600  md5(md5($pass))                                         | Raw Hash, Salted and/or Iterated
 3910  md5(md5($pass).md5($salt))                              | Raw Hash, Salted and/or Iterated
 4300  md5( $strupper(md5($pass)))                             | Raw Hash, Salted and/or Iterated
 4400  md5(sha1($pass))                                        | Raw Hash, Salted and/or Iterated
 110  sha1($pass.$salt)                                       | Raw Hash, Salted and/or Iterated
 120  sha1($salt.$pass)                                       | Raw Hash, Salted and/or Iterated
 130  sha1( utf16le($pass).$salt)                             | Raw Hash, Salted and/or Iterated
 140  sha1($salt.utf16le($pass))                              | Raw Hash, Salted and/or Iterated
```

Hashcat is a very powerful tool with a myriad of features. If you look at its help screen, it runs on for pages.

```
kali > hashcat -help 135 | P a g e
```