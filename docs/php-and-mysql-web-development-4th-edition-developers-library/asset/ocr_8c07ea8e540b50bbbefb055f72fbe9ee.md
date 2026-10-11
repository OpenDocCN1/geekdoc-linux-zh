```
AES_DECRYPT(AES_ENCRYPT('secret','scramble'),'scramble')
→ 'secret'
```

+   - `AES_ENCRYPT(str,key_str)`
+     Encrypts the string *str* with the key string *key_str* using the Advanced Encryption Standard (AES) and a 128-bit key length. Returns the result as a binary string, or NULL if either argument is NULL. The string may be decoded with `AES_DECRYPT()`, using the same key string.

+   - `COMPRESS(str)`
+     Returns a compressed version of the argument string as a binary string, or NULL if the server was not compiled with a compression library.

+   - `DECODE(str,key_str)`
+     Given an encrypted string *str* obtained as a result of a call to `ENCODE()`, decrypts it using the key string *key_str*. Returns the resulting string, or NULL if *str* is NULL.

```
DECODE(ENCODE('secret','scramble'),'scramble')
→ 'secret'
```

+   - `DES_DECRYPT(str [,key_str])`
+     Decrypts a string *str*, which should have an encrypted value produced by `DES_ENCRYPT()`. If SSL support has not been enabled or decryption fails, `DES_DECRYPT()` returns NULL.
+   
+   If a *key_str* argument is given, it is used as the decryption key. If no *key_str* argument is given, `DES_DECRYPT()` uses a key from the server’s DES key file to decrypt the string. The key number is determined from bits 0-6 of the first byte of the encrypted string. The location of the key file is specified at server startup time by means of the `--des-key-file` option. If different keys are used to encrypt and decrypt the string, the result will not be meaningful.
+   
+   If *str* does not look like an encrypted string, `DES_DECRYPT()` returns the string unchanged. (This will occur, for example, if the first byte does not have bit 7 set.)
+   Use of the single-argument form of `DES_DECRYPT()` requires the `SUPER` privilege.

+   - `DES_ENCRYPT(str [, (key_num|key_str)])`
+     Performs DES encryption on the string *str* and returns the encrypted result as a binary string. The encrypted string may be decrypted with `DES_DECRYPT()`. If SSL support has not been enabled or encryption fails, `DES_ENCRYPT()` returns NULL.
+   
+   If a *key_str* argument is given, it is used as the encryption key. If a *key_num* argument is given, it should be a value from 0 to 9, indicating the key number of an entry in the server’s DES key file. In this case, the encryption key is taken from that entry. If no *key_str* or *key_num* argument is given, the first key from the DES key file is used to perform encryption. (This is not necessarily the same as specifying a *key_num* value of 0.)