ciphertext, bits of information about the key can be obtained. Obviously, the more pairs of plaintext and ciphertext one has, the greater chance of success. Linear cryptanalysis is based on finding affine approximations to the action of a cipher. It is commonly used on block ciphers.

Remember cryptanalysis is an attempt to crack cryptography. For example, with the 56-bit DES key, brute force could take up to 2^56 attempts. Linear cryptanalysis will take 2^47 known plaintexts.^1 This is better than brute force, but still impractical for most situations.

# Steganography

Steganography is the art and science of writing hidden messages in such a way that no one, apart from the sender and intended recipient, suspects the existence of the message; this is a form of security through obscurity. The message is often hidden in some other file such as a digital picture or audio file, so as to defy detection.

The advantage of steganography, over cryptography, is that messages do not attract attention to themselves. If no one is aware the message is even there, they won't even try to decipher it. In many cases messages are encrypted and hidden via steganography.

The most common implementation of steganography utilizes the least bits in a file in order to store data. By altering the least significant bit, one can hide additional data without altering the original file in any noticeable way.

Here are some basic steganography terms you should know:

+   * Payload is the data to be covertly communicated. In other words, it is the message you want to hide.
* The carrier is the signal, or data file into which the payload is hidden.
* The channel is the type of medium used. This might still be photos, video, or sound files.

Although the use of digital steganography is obviously recent, the concept of hiding messages is not. Here are some instances of historical hidden messages:

+   * The ancient Chinese wrapped notes in wax and swallowed them for transport.
* In ancient Greece a messenger's head was shaved, a message written on his head, his hair was allowed to grow back.
* In the early 1500s Johannes Trithemius wrote a book on cryptography and described a technique where a message was hidden by having each letter as a word from a specific column.