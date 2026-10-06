
## Learning About Modern Encryption Methods

Modern cryptography methods, as well as computers, make decryption a rather advanced science. Therefore, encryption must be equally sophisticated in order to have a chance of success.

What you have seen far regarding encryption is simply for educational purposes. As has been noted several times, you would not have a truly secure system if you implemented any of the previously mentioned encryption schemes. You might feel that this has been overstated in text. However, having an accurate view of what encryption methods do and do not work is critical. It is now time to discuss a few methods that are actually in use today.

The following websites offer more information about cryptography:

- Cryptography course on Coursera: https://www.coursera.com/course/crypto
- Applied cryptography course on Udacity: https://www.udacity.com/course/applied-cryptography--cs387
- Cipher Research Laboratories: www.cypher.com.au/crypto_history.htm

Understanding the simple methods described here and other methods provided by the aforementioned websites would give you a sense of how cryptography works as well as what is involved in encrypting a message. Regardless of whether you go on study modern, sophisticated encryption methods, having some basic idea of how encryption works at a conceptual level is important. Having a basic grasp of how encryption works, in principle, will make you better able to understand the concepts of any encryption method you encounter in the real world.

> FYI: Careers in Cryptography

Some readers might be interested in a career in cryptography. Basic knowledge of cryptography is enough to be a security administrator, but not enough to be a cryptographer. A strong mathematics background is essential for in-depth exploration of cryptography, particularly when pursuing a career in this field. An adequate background includes a minimum of the complete calculus sequence (through differential equations), statistics through basic probability theory, abstract algebra, linear algebra, and number theory. A double major in computer science and mathematics is ideal. A minimum of a minor in mathematics is required, and familiarity with existing encryption methods is critical.

## Learning About Modern Encryption Methods

Not surprisingly, modern methods of encryption are more secure than the historical methods just discussed. All the methods discussed in this section are in use today and are considered reasonably secure. Note that DES is an encryption, but only due to its key length.

## CHAPTER 6 Encryption Fundamentals

In some cases the algorithm behind these methods requires a sophisticated understanding of mathematics. Number theory often forms the basis for encryption algorithms. Fortunately for our purposes having the exact details of these encryption algorithms is not important; this means you don't require a strong mathematics background to follow this material. More important is a general understanding of how a particular encryption method works and how secure it is.

## Symmetric Encryption

Symmetric encryption refers to those methods where the same key is used to encrypt and decrypt the plaintext.

## Data Encryption Standard

Data Encryption Standard, or DES as it is often called, was developed by IBM in the early 1970s and made public in 1976. DES uses a symmetric key recall. From our earlier discussion that this means the same key is used to encrypt and decrypt the message. DES uses short keys and relies on complex procedures to protect its information. The actual DES algorithm is quite complex. The basic concept, however, is as follows:

1. The data is divided into 64-bit blocks, and those blocks are transposed.
2. Transposed data is manipulated by 16 separate rounds of encryption, involving substitutions, bit-shifting, and logical operations using a 56-bit key.
3. Finally, the data is transposed one last time.

More information about DES is available at the Federal Information Processing Standards website at https://csrc.nist.gov/csrc/media/publications/fips46/3/archive/1999-10-25/documents/fips46-3.pdf. A detailed description of DES is given below, but you can skip this if you wish.

DES uses a 56-bit cipher applied to a 64-bit block. There is actually a 64-bit key, but one bit of every is actually used for error detection, leaving 56 bits for actual operations.

DES is a Feistel cipher with 16 rounds and a 48-bit key for each round. A round key is just a sub key that is derived from the cipher key round, according to a key schedule. DES's general functionality follows the Feistel method of dividing the 64-bit block into two halves (32 bits each; this is not an unbalanced Feistel cipher), applying the round function to one half, then XORing with the other half.

The first issue is the key schedule. How does DES generate a new sub key each round? The idea is to take the original 56-bit key and permute it each round so that each round is a slightly different key, but one that is based on the original key. To generate the rounds, the 56-bit is split into two 28-bit halves and halves are circularly shifted after each round by one or two bits. This will provide a sub key each round. During the key generation portion of the algorithm(which this is referred to as the key schedule) each round, the two halves of the original cipher key (the 56 bits of the two endpoints of encryption must exchange) are shifted a specific amount.

## Learning About Modern Encryption Methods

Once the round key has been generated for the current round, the next step is to address the half of the original block that is going to be input into the round function. Recall that the two halves are each 32 bits. The round key is 48 bits. That means the round key does not match the size of the half block it is going to. You cannot XOR a 48-bit round key with a 32-bit block unless you simply ignore 16 bits of the round key. If you did, you would basically be making the round key shorter and less secure. The 32-bit half needs to be expanded to 48 bits before it is XORed with the round key. This is accomplished by replicating bits so that the 32-bit half becomes 48 bits. This expansion is actually simple. The 32 bits are be broken into 4-bit sections. The bits on each end are duplicated. If you divide 32 by 4 the answer is 8. So there are eight of these 4-bit groupings. If you duplicate the bits of each grouping, that will add 16 bits to the original 32, providing a total of 48 bits. It is also important to keep in mind that the bits on each end were duplicated; this will be the round function. Perhaps this example will help you understand what is occurring at this point.

111001101011111100101001

Now divide into eight sections of 4 bits:

1111001101011111101001

Now each of these has its ends duplicated:

111111
001111
010111
111111
111111
000111
100111

The resultant 48-bit string is now XORed with the 48-bit key. That is the round key used in each round. It is now dispensed and on the next round another 48-bit key will be derived from the two 28-bit halves of the 56-bit cipher key. Now we have the 48-bit output of the XOR operation split into eight sections of 6 bits. For the rest of this explanation we will focus on just one of those 6-bit sections, but keep in mind that the same process is done to all eight.

## CHAPTER 6 Encryption Fundamentals

The 6-bit section is used as the input to an s-box. An s-box is a table that takes and produces an output based on that input. In other words, it is a substitution box that substitutes new values for the input. The s-boxes used in DES, the first of which is shown in Figure 6-1.

| | 000000 | 000001 | 000010 | 000011 | 000100 | 000101 | 000110 | 000111 | 001000 | 001001 | 001010 | 001011 | 001100 | 001101 | 001110 | 001111 |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| 0yyyyyy | 12 | 1 | 15 | 10 | 9 | 2 | 6 | 8 | 0 | 13 | 3 | 4 | 14 | 7 | 5 | 11 |
| 0yyyyyl | 15 | 4 | 2 | 12 | 9 | 5 | 6 | 1 | 13 | 4 | 10 | 11 | 3 | 8 |
| 0yyyyx | 9 | 14 | 15 | 2 | 12 | 3 | 4 | 10 | 13 | 11 | 0 | |
| 1yyyyy | 4 | 3 | 12 | 9 | 5 | 19 | 10 | 11 | 14 | 7 | 6 | 0 | 13 |

FIGURE 6-1 The DES s-box

Notice this is a lookup table. The 2 bits on either end are shown in the left hand and the 4 bits in the middle are in the top row. They are matched, and the resulting value is the output of the s-box. For example, with the previous demonstrations we were using, our first block would be 111111. If you find ixxxx on the left and x111x on the top, the resulting value is 13 in decimal or 1101 in binary.

At the end of this you have produced 32 bits that are the output of the round function. In keeping with the Feistel structure, you XORed with the 32 bits that were not into the round function, and the two halves are swapped. DES is a 16-round Feistel cipher, meaning this process is repeated 16 times.

There are only two parts left to consider regarding DES. The first is the initial permutation, called the IP, then the inverse of the IP.

One advantage of DES is efficiency. Some implementations of DES offer data throughput on the order of hundreds of megabytes per second. In plain English, what this means is that it can encrypt a great deal very quickly. You might assume that 16 steps would cause encryption to be quite slow; however, that is not the case using modern computer equipment. The problem with DES is the same as all other symmetric algorithms: How do you transmit the key without becoming compromised? This issue led to the development of public key encryption.
