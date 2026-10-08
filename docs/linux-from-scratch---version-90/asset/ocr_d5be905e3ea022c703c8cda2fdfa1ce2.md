# 5.25. Grep-3.3

The Grep package contains programs for searching through files.
Approximate build time: 0.2 SBU
Required disk space: 24 MB

# 5.25.1. Installation of Grep

Prepare Grep for compilation:

```
.//configure --prefix=/tools
```

Compile the package:

```
make
```

Compilation is now complete. As discussed earlier, running the test suite is not mandatory for the temporary tools here in this chapter. To run the Grep test suite anyway, issue the following command:

```
make check
```

Install the package:

```
make install
```

Details on this package are located in Section 6.33.2, "Contents of Grep."