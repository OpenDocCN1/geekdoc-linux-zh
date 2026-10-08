# Hacking Exposed Web Applications

A “less” secure “more” and “less” are ill-defined terms in cryptography but equally viable method would only use the server's secret and the user's password:

```
MD5( secret + password )
```

In this case, the user needs to guess the server's secret. If the secret value is less than characters, a successful attack by a single malicious user is conceivable.

DES A session token encrypted by DES or Triple-DES is hard to identify. The values may appear, but they might concentrate around certain loci. There's no hard-and-fast rule for identifying the algorithm used to encrypt a string. There are no length limitations to the encryption, although multiples of eight bytes tend to be used. The only thing you can do is guess the contents, compare it, and compare it with the string in question.

Just because you cannot decrypt a value does not preclude you from guessing content or noticing trends. For example, you might collect a series of session tokens that only differ in certain parts:

+   - 4GjxrFab0AvcfgpSY3FotMgbro
- 4miESPG64AvcfgpSY3FotMgbW
- 4e2nCZ5AvcfgpSY3FotMgbpr
- 4w1lsjsisAvcfgpSY3FotMgbok
- 4CdVgbZalAvcfgpSY3FotMgbH
- 4JfqToEzBAvcfgpSY3FotMgb7
- 4P9TCCyAaVcfgpSY3FotMgb
- 4WmEoltngAvcfgpSY3FotMgbnW
- 46W8VtZCAAvcfgpSY3FotMgbhI
- 4miFHDtyAvcfgpSY3FotMgbJv
- 4tqnorisDAVcfgpSY3FotMgbVg
- 4z8DAEYHhcAvcfgpSY3FotMgb3

Did you notice the? Each value begins with the number four. If it is an encrypted string, there are eight bytes after the four, fourteen bytes do not change, by a final two random bytes. If this is an encrypted string, then we could make some guesses about its random bytes. We'll assume it's encrypted with Triple-DES, since DES is known to be weak:

```
String = digit + 3DES( nonce + username (+ flags) + counter )
            4             8 bytes         2 bytes
```

Here's why we make the assumption:

+   - The field of eight characters always changes. The values are encrypted, so we have no way of knowing if they increment, decrement, or are truly random.
Anyway, the source must be changing so we'll refer to it as a nonce.