# Atbash Cipher

Hebrew scribes copying the book of Jeremiah used the Atbash cipher. Using it is simple; you just reverse the alphabet. This is, by modern standards, a primitive and easy-to-break cipher. However, it will help you get a feel for how cryptography works.

The Atbash cipher is a Hebrew code that substitutes the first letter of the alphabet for the last the second letter for the second to last, etc. It simply reverses the alphabet; for example, A becomes Z, B becomes Y, C becomes X,

This, like the Caesar cipher and ROT 13 ciphers, is also a single-substitution cipher.

# Multi-Alphabet Substitution

Eventually, a slight improvement over the Caesar cipher was developed, called multi-alphabet substitution (also called polyalphabetic substitution). In this scheme, you select multiple numbers by which to shift letters (that is, multiple-substitution alphabets). For example, if you select three alphabets (12, 22, 13), then

+   A CAT

+   becomes

+   C ADV

Notice that the fourth letter starts with another 12, and you can see that the first A was transformed to C and the second A was transformed to D. This makes deciphering the underlying text much difficult. Although this is harder to decrypt than a Caesar cipher, it is not overly difficult to decode. It can be done with simple pen and paper and a bit of effort. If it can be cracked quickly with a computer, no one would use such a method today to send any secure message, for this type of encryption is considered very weak.

One of the most widely known multi-alphabet ciphers is the Vigenere. This topic is discussed in detail later in this chapter. This cipher was invented in 1553 by Giovanni Bellaso. It is a method of encrypting alphabetic text using a series of different mono-alphabetic ciphers selected based on the letters of a key. This algorithm was widely misattributed to Blaise de Vigenere, and so it is known as the "Vigenere cipher," even though Vigenere did not invent it.

Multi-alphabet ciphers are more secure than single-substitution ciphers. However, they are still not acceptable for modern cryptographic usage. Computer-based cryptanalysis systems can crack historical cryptographic methods (both single substitution and multi-alphabet) easily. The single-substitution alphabet alphabets are discussed just to show the history of cryptography, and to help you get an understanding of how cryptography works.

# Rail Fence

All the preceding ciphers we examined are substitution ciphers. Another approach to classic cryptography is the transposition cipher. The rail fence cipher may be the most widely known transposition