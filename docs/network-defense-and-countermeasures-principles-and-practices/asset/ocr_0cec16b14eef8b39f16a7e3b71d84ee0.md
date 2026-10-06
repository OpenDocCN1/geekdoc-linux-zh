# CHAPTER 6 Encryption Fundamentals

+   - SHA-2: This is actually two similar hash functions, in the word size, known as SHA-256 and SHA-512. They differ in the word size; SHA-256 uses 32-byte (256 bits) words whereas SHA-512 uses 64-byte (512 bits) words. There are also truncated of each standard, known as SHA-224 and SHA-384. These were also designed by the NSA.

+   - SHA-3: This is the latest version of SHA. It was adopted in October of 2012.

# RIPEMED

RACE Integrity Primitives Evaluation Message Digest is a 160-bit hash algorithm developed by Hans Dobbertin, Anton Booselaar, and Bart Prenel. There exist 128-, 256-, and 320-bit versions of this algorithm, called RIPEMED-128, RIPEMED-256, and RIPEMED-320, respectively. These all replace the original RIPEMED, which was found to have collision issues. The larger bit sizes make this far more secure than MD5 or RIPEMED.

RIPEMED-160 was developed in Europe as part of RIPE project and is recommended by the German Security Agency. The authors of the algorithm describe RIPEMED as “RIPEMED-160 is a fast cryptographic hash function that is tuned towards software implementations on 32-bit architectures. It has evolved from the 256-bit extension of MD4, which was introduced in 1990 by Ron Rivest. Its main features are two different independent parallel channels, the result of which are achieved at the end of every application of the compression function.” To read the authors’ full explanation of RIPEMED-160, see www.esat.kuleven.be/cosic/publications/article-317.pdf.

# HAVAL

HAVAL is a cryptographic hash function. Unlike MD5, but like other modern cryptographic hash functions, HAVAL can produce hashes of different lengths. HAVAL can produce hashes in lengths of 128 bits, 160 bits, 192 bits, 224 bits, and 256 bits. HAVAL also allows users to specify the number of rounds (3, 4, or 5) to be used to generate the hash. HAVAL was invented by Yuliang Zheng, Josef Pieprzyk, and Jennifer Seberry in 1992.

# Understanding and Using Decryption

Obviously, if one can encrypt a message, one can decrypt it as well. The preferred method is, of course, to have the key and the algorithm, and hopefully the software used to encrypt and then easily decrypt the message. However, people attempting to breach your security will not have the algorithm and key and will want to break your encrypted transmissions or data.

Decryption is a science like encryption. It employs various mathematical methods to crack encryption. You can find a number of utilities on the web that actually crack encryption for you. As discussed earlier, no such exists as unbreakable encryption. However, the more secure an