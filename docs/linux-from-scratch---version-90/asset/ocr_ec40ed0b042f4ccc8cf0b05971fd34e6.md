# 5.18. Bzip2-1.0.8

The Bzip2 package contains compression programs for compressing and decompressing files.  Compressing text files with bzip2 yields a much better compression percentage than with the traditional gzip.

**Approximate build time:** less than 0.1 SBU
**Required disk space:** 6.0 MB

# 5.18.1. Installation of Bzip2

The Bzip2 package does not contain a **configure** script. Compile and test it with:

```
make
```

Install the package:

```
make PREFIX=/tools install
```

Details on this package are located in Section 6.22.2, “Contents of Bzip2.",