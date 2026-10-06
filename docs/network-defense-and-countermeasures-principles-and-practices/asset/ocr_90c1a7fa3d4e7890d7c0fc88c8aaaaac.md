# Frequency Analysis

Frequency analysis involves looking at blocks of an encrypted message to determine if any common patterns exist. Initially, the analyst doesn't try to break the code but looks at the patterns in the message. In the English language, the letters e and t and words like the, and, that, it, and are very common. Single letters that stand alone in a sentence are usually limited to a and I.

A determined cryptanalyst looks for these types of patterns and, over time, may be able to deduce the method used to encrypt the data. This process can sometimes be simple, or it may take a lot of effort. This method works only on the historical ciphers we discussed at the beginning of this chapter. It does not work on modern algorithms.

# Known Plaintext

This attack relies on the attacker having pairs of known plaintext along with the corresponding ciphertext. This gives the attacker a place to start attempting to derive the key. With modern ciphers, it would still take billions of combinations to have a chance at cracking the cipher. This method was, however, successful at cracking the German Naval Enigma. The code breakers at Bletch Park realized that all German Naval messages ended with Heil Hitler. They used this known plaintext attack to crack the key.

# Chosen Plaintext

In this attack, the attacker obtains the ciphertexts corresponding to a set of plaintexts of their choosing. This allows the attacker to attempt to derive the key and decrypt other messages encrypted with that key. This can be difficult, but it is not impossible. Advanced methods such as differential cryptanalysis are types of chosen plaintext attacks.

# Known Key Attack

This is like a chosen-plaintext attack, except the attacker can obtain ciphertexts encrypted under two different keys. This is actually a very useful attack if you can obtain the plaintext and matching ciphertext.

# Birthday Attack

This is an attack on cryptographic hashes, based on something called the birthday theorem. The basic idea is this: how many people would you need to have in a room to have a strong likelihood that two people would have the same birthday (month and day, but not year)?

Obviously, if you put 367 people in a room, at least 2 of them must have the same birthday, since there are only 365 days in a year, plus one more in a leap year.

The paradox is not asking how many people you need to guarantee a match, just how many you need to have a strong probability.