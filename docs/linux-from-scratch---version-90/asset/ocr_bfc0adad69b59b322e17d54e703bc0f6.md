# 5.31. Sed-4.7

The Sed package contains a stream editor.
Approximate build time: 0.2 SBU
Required disk space: 20 MB

# 5.31.1. Installation of Sed

Prepare Sed for compilation:

```
./configure --prefix=/tools
```

Compile the package:

```
make
```

Compilation is now complete. As discussed earlier, running the test suite is not mandatory for the temporary tools here in this chapter. To run the Sed test suite anyways, issue the following command:

```
make check
```

Install the package:

```
make install
```

Details on this package are located in Section 6.28.2, “Contents of Sed."