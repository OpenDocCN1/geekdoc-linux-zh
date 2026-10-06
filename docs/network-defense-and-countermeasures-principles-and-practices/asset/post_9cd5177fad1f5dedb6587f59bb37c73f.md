
## Blowfish

Blowfish is a symmetric block cipher. This means it uses a single key to both encrypt and decrypt the message and works on “blocks” of the message at a time. It uses a variable-length key ranging from 32 to 448 bits. This flexibility in key size allows you to use it in various situations. Blowfish was designed in 1993 by Bruce Schneier. It has been analyzed extensively by the cryptography community and has gained wide acceptance. It is also a non-commercial (that is, free of charge) product, thus making it attractive to budget-conscious organizations.

> FYI: Block Ciphers and Stream Ciphers

A block cipher operates on blocks of fixed length, often 64 or 128 bits. In a block cipher, a cryptographic key and algorithm are applied to a block of data (for example, 64 contiguous bits) at once as a group rather than one at a time. Stream ciphers simply take the text as an ongoing stream, encrypting each bit as it encounters it. Stream ciphers tend to be faster than block ciphers. A stream cipher generates a keystream (a sequence of bits used as a key). Encryption is accomplished by combining the keystream with the plaintext, usually with the XOR operation.

## AES

Advanced Encryption Standard (AES) uses the Rijndael algorithm. The developers of this algorithm have suggested multiple alternative pronunciations for the name, including “reign dahl.” “rain doll,” and “thine dahl.” This algorithm was developed by two Belgian researchers, Joan Daemen of Proton World International and Vincent Rijmen, a postdoctoral researcher in the Electrical Engineering Department of Katholie Universiteit Leuven.

AES specifies three key sizes: 128, 192, and 256 bits. By comparison, DES keys are 56 bits, and Blowfish allows varying lengths up to 448 bits. AES uses a block cipher. Interested readers can find detailed specifications of this algorithm, the mathematics, at https://www.nist.gov/csrc/csrc/publications/fips/197/final/documents/fips-197.pdf.

This algorithm is widely used (as in the firewall discussion in Chapter 4, “Firewall Applications”), considered very secure, and therefore a good choice for many encryption scenarios.

For those who want more detail, here is a general overview of the process used in AES. The algorithm consists of a few relatively simple steps that are used during various rounds. The steps are described here:

- AddRoundKey: Each byte of the state is combined with the round key using bitwise XOR. This is where Rijael applies the round key generated from the key schedule.

- SubBytes: A nonlinear substitution step where each byte is replaced with another according to a lookup table. This is where the contents of the matrix are put through the s-boxes. Each of the s-boxes is 8 bits.

- ShiftRows: A transposition step where each row of the state is shifted cyclically a certain number of steps. In this step the first row is left unchanged. Every byte in the second row is shifted one byte to the left (with the far left wrapping around). Every byte of the third row is shifted two to the left, and every byte of the fourth row is shifted to the left (again with wrapping around).

- MixColumns: A mixing operation that operates on the columns of the state, combining the 4 bytes in each column. In the MixColumns step, each column of the state is multiplied with a fixed polynomial.

With the aforementioned steps in mind, this is how steps are executed in the Rijndael cipher. 128-bit keys, there are 10 rounds. For 192-bit keys, there are 12 rounds. For 256-bit keys, there are 14 rounds.

- Key Expansion: The first step is that the round keys are derived from the cipher key using Rijndael's key schedule. The key schedule is how a key is generated for each round, based on the cryptographic key that was exchanged between the sender and receiver.

- Initial Round: This initial round will only execute the AddRoundKey step. This is simply XORing with the round key. This initial round is executed once, then the subsequent rounds will be executed.

- Rounds: This phase of the algorithm executes several steps, in the following order:

- SubBytes
- ShiftRows
- MixColumns
- AddRoundKey

- Final Round: This round has everything the rounds phase, except no MixColumns.

- SubBytes
- ShiftRows
- AddRoundKey

In the AddRoundKey step, the sub-key is XORed with the state. For each round, a sub-key is derived from the main key using Rijndael's key schedule; each sub-key is the same size as the state.

## IDEA

International Data Encryption Algorithm (IDEA) is another block cipher. This particular algorithm works with 64-bit blocks of data at a time and a 128-bit key. The procedure is fairly complicated and uses sub-keys generated from the key to carry out a series of modular arithmetic and XOR operations on segments of the 64-bit plaintext block. The encryption scheme uses a total of 52 16-bit sub-keys. These are generated from the 128-bit key with the following procedure:

- 128-bit key is split into eight 16-bit keys, which are the first eight sub-keys.

- The digits of the 128-bit key are shifted 25 bits to the left to make a new key, which is then split into the next eight 16-bit sub-keys.

- The second step is repeated until the 52 sub-keys have been generated. The encryption consists of eight rounds of encrypting.

## Serpent

This algorithm was invented by Ross Anderson, Eli Biham, and Lars Knudsen. It was submitted to the AES competition but was not selected, in large part due to the fact that its performance is slower than AES. However, in the ensuing years since the AES competition, computational power has increased dramatically. This has led some experts to reconsider the use of Serpent on modern systems.

## Twofish

Twofish was one of the finalists of the AES contest (which we will explore in more detail in Chapter 7, “Virtual Private Networks”). It is related to the cipher Blowfish, and Bruce Schneier was also part of the team that worked on this algorithm. Twofish is a Feistel cipher that uses a 128-bit block size and keys of 128, 192, and 256 bits. It also has 6 rounds, like DES. Like Blowfish, Twofish is not patented and is in the public domain and can be used without restrictions by anyone who wishes to use it.

## Selecting a Block Cipher

If you have decided on a block cipher, which one do you choose? We have examined several here, all with different strengths and weaknesses. No single answer is right for everyone. Several factors are involved in the selection of an encryption algorithm. Here are a few things to keep in mind:

- If you encrypt large amounts of data, then the speed of the encryption might be almost as important as security.

- If you have standard business data, then any of the well-known encryption methods will probably be secure, and you can focus on things as key length and speed in your decision-making process. If you are handling highly sensitive data, such as research or military data, you should be more concerned about security, even at the expense of speed.

- Variable-length keys are important only if you need them. If you have some encryption products used inside the United States and outside, then at least two lengths are needed. If you have some data you need strongly encrypted if it means slower speed, and data that needs to be fast but not as secure, then a variable-length key is also important.

## Key Stretching

It is sometimes necessary to lengthen a key to make it stronger. This process is often called key stretching. The key is put through an algorithm that will stretch it, or make it longer. There are two widely used key stretching algorithms:

- KDF2 (Password-Based Key Derivation Function 2) is part of PKCS #5 v 2.01. It applies some function (like a hash or HMAC) to the password or passphrase along with salt to produce a derived key. (The concept is discussed later, in the “Hashing” section)
