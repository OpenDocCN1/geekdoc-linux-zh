+   - **ECC** - Elliptical curve cryptography is becoming increasing popular in mobile computing as it efficient, requiring less computing power and energy consumption for the same level of security. ECC relies upon the shared relationship of two functions being on the same elliptical curve.

+   - **PGP** - Pretty Good Privacy uses asymmetric encryption to assure the privacy and integrity of email messages.

# Hashes

Hashes are one-way encryption. A message or password is encrypted in a way that it cannot be reversed or unencrypted. You might wonder, "What good would it do us to have a something encrypted and then not be able to decrypt it?" Good question!

When the message is encrypted it creates a "hash" that becomes a unique, but indecipherable signature for the underlying message. Each and every message is encrypted in a way that it creates a unique hash.

Usually, these hashes are a fixed length (an MD5 hash is always 32 characters). In that way, the attacker can not decipher any information about the underlying message from the length of the hash. Due to this, we don't need to know the original message, we simply need to see whether some text creates the same hash to check its integrity (is unchanged).