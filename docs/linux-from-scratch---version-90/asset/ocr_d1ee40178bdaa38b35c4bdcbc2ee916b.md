# # 6.21. GCC-9.2.0

The GCC package contains the GNU compiler collection, which includes the C and C++ compilers.

Approximate build time: 95 SBU (with tests)
Required disk space: 4.2 GB

# ## 6.21.1. Installation of GCC

If building on x86_64, change the default directory name for 64-bit libraries to "lib":

```
case $(uname -m) in
  x86_64)
    sed -e '/m64/s/lib64/lib/' '\'
      -i.orig gcc/config/i386/t-linux
    ;;
esac
```

The GCC documentation recommends building GCC in a dedicated build directory:

```
mkdir -v build
cd build
```

Prepare GCC for compilation:

```
SED=sed
./configure --prefix=/usr
  --enable-languages=c,c++
  --disable-multilib
  --disable-bootstrap
  --with-system-zlib
```

Note that for other languages, there are some prerequisites that are not yet available. See the BLFS Book for instructions on how to build all of GCC’s supported languages.

**The meaning of the new configure parameters:**

```
SED=sed
Setting this environment variable prevents a hard-coded path to /tools/bin/sed.
--with-system-zlib
This switch tells GCC to link to the system installed copy of the Zlib library, rather than its own internal copy.
```

Compile the package:

```
make
```

> **Important**
In this section, the test suite for GCC is considered critical. Do not skip it under any circumstance.