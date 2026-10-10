In the listing above, the Debian installer image files are accompanied by text files that contain checksums of the files from the various algorithms (MD5, SHA1, SHA256 and SHA512).

> **NOTE**
> A checksum is a value derived from a mathematical computation, based on a cryptographic hash function, against a file. There are different types of cryptographic hash functions that vary in strength. The exam will expect you to be familiar with using md5sum, sha256sum and sha512sum.

Once you download a file (for example, the debian-10.1.0-amd64-netinst.iso image) you would then compare the checksum of the file that was downloaded against a checksum value that was provided for you.

Here is an example to illustrate the point. We will calculate the SHA256 value of the ftu.txt file using the sha256sum command:

```
$ sha256sum ftu.txt
345452304fc26999a715652543c352e5fc7ee0c1b9deac6f57542ec91daf261c  ftu.txt
```

The long string of characters preceding the file name is the SHA256 checksum value of this text file. Let us create a file that contains that value, so that we can use it to verify the integrity of our original text file. We can do this with the same sha256sum command and redirect the output to a file:

```
$ sha256sum ftu.txt > sha256.txt
```

Now, to verify the ftu.txt file, we just use the same command and supply the filename that contains our checksum value along with the -c switch:

```
$ sha256sum -c sha256.txt
ftu.txt: OK
```

The value contained within the file matches the calculated SHA256 checksum for our ftu.txt file, just as we would expect. However, if the original file were modified (such as a few bytes lost during a file download, or someone had deliberately tampered with it) the value check would fail. In such cases we know that our file is bad or corrupted, and we can not trust the integrity of its contents. To prove the point, we will add some text at the end of the file:

```
$ echo "new entry" >> ftu.txt
```