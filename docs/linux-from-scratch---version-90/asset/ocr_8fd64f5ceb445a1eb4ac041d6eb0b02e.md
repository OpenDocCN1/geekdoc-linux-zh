# ## 6.66. Make-4.2.1

The Make package contains a program for compiling packages.
Approximate build time: 0.6 SBU
Required disk space: 13 MB

# ### 6.66.1. Installation of Make

Again, work around an error caused by glibc-2.27 and:

```
sed -i '211,217 d; 219,229 d; 232 d' glob/glob.c
```

Prepare Make for compilation:
To test the results, issue:

```
./configure --prefix=/usr
```

Compile the package:
The test suite needs to know where supporting perl files are located. We use an environment variable to accomplish this.

```
make PERL5LIB=$PWD/tests/ check
```

Install the package:

```
make install
```

# ### 6.66.2. Contents of Make

Installed program:    make

# #### Short Descriptions

make Automatically determines which pieces of a package need to be (re)compiled and then issues the relevant commands