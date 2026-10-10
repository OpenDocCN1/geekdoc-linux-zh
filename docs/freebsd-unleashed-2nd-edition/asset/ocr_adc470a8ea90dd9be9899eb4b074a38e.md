# **LISTING 14.2 Verbose Output of pkg_info**

```
# pkg_info -v pgp-2.6.3ia
Information for pgp-2.6.3ia:

Comment:
PGP MIT or International version - Public-Key encryption for the masses

Depends on:
Description:
PGP (Pretty Good Privacy) is a public key encryption pack-
age to protect E-mail and data files. It lets you commu-
nicate securely with people you've never met, with no
secure channels needed for prior exchange of keys. It's
well featured and fast, with sophisticated key management,
digital signatures, data compression, and good ergonomic
design.

WWW: http://www.pgpi.org/

Packing list:
Package name: pgp-2.6.3ia
CWD to /usr/local
File: man/man1/pgp.1.gz
Comment: MD5:a0ab17d1fe83aafl59cb80fa1abf5462
File: bin/pgp
Comment: MD5:625e99562f936a9d9b0c3c5d5a94ba9
File: lib/pgp/pgp.hlp
Comment: MD5:d5da3783ea26cb6f04b7584df4227866
File: lib/pgp/pgpdocl.txt
Comment: MD5:260ca85cd0263275cb7df6cd276e2b9f
File: lib/pgp/pgpdoc2.txt
Comment: MD5:e3defe467bf5c5c4809f8b5c13404a1
File: lib/pgp/language.txt
Comment: MD5:bce0f56b207846725fe7e4a612083ef
File: lib/pgp/config.txt
Comment: MD5:b2518ad2566a9a4bce071936311d3c93
Deinstall directory remove: lib/pgp
UNEXEC 'if [ -f %D/info/dir ]; then if sed -e '1,/Menu:/d' 
_%D/info/dir | grep -q '^[*] '; then true; else rm %D/info/dir; fi; fi'
```

This listing tells you everything you need to know about the package—from its long description, to its dependencies, to its packing list (with the MD5 “fingerprint” checksum for each file, listed in its Comment field). Some files have extra information noted, such as