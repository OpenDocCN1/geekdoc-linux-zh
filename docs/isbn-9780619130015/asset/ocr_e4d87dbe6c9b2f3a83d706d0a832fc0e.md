![](bbox=[0.2, 0.07, 0.8, 0.45])

Figure 10-13: Output of keyboard program

Now that you have created C programs that perform keyboard and file I/O, you are ready to write the security demonstration programs.

# ## Encoding and Decoding Programs

If a file contains sensitive information, you may wish to encrypt it so others cannot read its contents. When a file is **encrypted**, its contents are encoded or modified in such a way that the original contents are not distinguishable. A formula is used to perform the encryption, so that an alternative **decryption** algorithm can restore the file to its original contents.

The program you have been asked to write for Dominion Consulting's programming staff will be simple in design. It will open a file, read a character from the file, add 10 to the character's ASCII value, and then write the character to a second file. This procedure repeats until all characters in the file have been read, modified, and written to the second file. The second file will be an encoded version of the first file.

The decoding program will work opposite of the way the encoding program works. It will read a character from the encrypted file, subtract 10 from its ASCII code, and write the character out to another file. This procedure repeats until all encrypted characters have been converted to their original state and stored in the second file.