+   MD5(str)

Calculates a 128-bit checksum from the string str based on the RSA Data Security, Inc. MD5 Message-Digest algorithm. The return value is a binary string consisting of 32 hexadecimal digits, or NULL if the argument is NULL.

```
MD5('secret') → '5ebe2294ecd0e0e8a6b7f690da2aee69'
```

See also the SHA1() function.

+   OLD_PASSWORD(str)

This function returns the encrypted password value that PASSWORD() returned prior to MySQL 4.1.

+   PASSWORD(str)

Given a string str, calculates and returns an encrypted password string of the form used in the MySQL grant tables. This is a non-reversible encryption.

```
PASSWORD('secret') → '14e5567abdb5135dcf9a70b3032c179a49ee7'
```

PASSWORD() does not use the same algorithm as the one used on Unix to encrypt user account passwords. For that type of encryption, use ENCRYPT().

If the old_passwords system variable is non-zero, PASSWORD() returns the password encrypted using the same hashing algorithm that was used prior to MySQL 4.1. In this case, PASSWORD() and OLD_PASSWORD() return the same value.

old_passwords can be enabled by using a SET GLOBAL old_passwords = 1 statement or by starting the server with the --old-passwords option.

+   SHA1(str)

```
SHA(str)
```

Calculates a 160-bit checksum from the string str using the Secure Hash Algorithm. The return value is a binary string consisting of 40 hexadecimal digits, or NULL if the argument is NULL.

```
SHA1('secret') → 'e59ef1a3ba1ccd1ea84e575caa474f3a663f05f4'
```

+   SHA2(str,hash_length)

This function is similar to SHA1(), but is more secure. It hashes the first argument, producing a result with a bit length indicated by the second argument. The hash length must be 224, 256, 384, or 512. The result is a binary string of the specified number of bits, represented as hexadecimal digits. The result is NULL if either argument is NULL or the hash length is invalid.

```
SHA2('secret',224) → '95c7fbc492ac5083afd62a564a3d104fc72c9140c3eb99ea6bf12'
```

SHA2() was introduced in MySQL 6.0.5.