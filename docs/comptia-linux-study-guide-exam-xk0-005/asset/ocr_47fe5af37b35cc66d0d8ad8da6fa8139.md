# Securing Hash Algorithms

The Secure Hash Algorithms (SHA) is a family of various hash functions. Though typically used for cryptography purposes, they can also be used to verify an archive file's integrity.

Several utilities implement these various algorithms on Linux. The quickest way to find them is using the method shown in Listing 12.23. Keep in mind that your particular distribution may store them in the /bin directory instead.

# Listing 12.23 Looking at the SHA utility names

```
$ ls -l /usr/bin/sha*?sum
/usr/bin/sha224sum
/usr/bin/sha256sum
/usr/bin/sha384sum
/usr/bin/sha512sum
$
```

Each utility includes the SHA message digest it employs within its name. Therefore, sha384sum uses the SHA-384 algorithm. These utilities are used in a similar manner to the md5sum command. A few examples are shown in Listing 12.24.

# Listing 12.24 Using sha512sum to check the original file

```
$ sha224sum Project4x.tar
c36f1632cd4966967a6daa787cdf1a2d64ee5592
4e3993c69d9e9d0 Project4x.tar
$
$ sha512sum Project4x.tar
6d2cf04ddb20c369c2bcc77db294eb60d401fb443
d327d776a17b477000efe46c00478caF25ec6fc09
833d2f8c8d5ab910534ff4f05b5cc63f88a992fa
eb3 Project4x.tar
$
```

Notice in Listing 12.24 the different hash value lengths produced by the different commands. The sha512sum utility uses the SHA-512 algorithm, which is the best to use for security purposes and is typically employed to hash salted passwords in the /etc/shadow file on Linux.

You can use these SHA utilities, just like the md5sum program was used in Listings 12.21 and 12.22, to ensure archive files' integrity. That way, backup corruption is avoided as well as any malicious modifications to the file.