# 6.19. MPC-1.1.0

The MPC package contains a library for the arithmetic of complex numbers with arbitrarily high precision and correct rounding of the result.

**Approximate build time:** 0.3 SBU
**Required disk space:** 22 MB

# 6.19.1. Installation of MPC

Prepare MPC for compilation:

```
./configure --prefix=/usr \
--disable-static \
--dodecdir=/usr/share/doc/mpc-1.1.0
```

Compile the package and generate the HTML documentation:

```
make
make html
```

To test the results, issue:

```
make check
```

Install the package and its documentation:

```
make install
make install-html
```

# 6.19.2. Contents of MPC

**Installed Libraries:** libmpc.so
**Installed Directory:** /usr/share/doc/mpc-1.1.0

# Short Descriptions

**libmpc** Contains complex math functions