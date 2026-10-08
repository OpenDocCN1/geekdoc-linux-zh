# 6.77. Eudev-3.2.8

The Eudev package contains programs for dynamic creation of device nodes.
Approximate build time: 0.2 SBU
Required disk space: 22 MB

# 6.77.1. Installation of Eudev

Prepare Eudev for compilation:

```
./configure --prefix=/usr \
--bindir=/sbin \
--sbindir=/sbin \
--libdir=/usr/lib \
--sysconfdir=/etc \
--libexecdir=/lib \
--with-rootlibprefix= \
--with-rootlibdir=/lib \
--enable-manpages \
--disable-static
```

Compile the package:

```
make
```

Create directories now that are needed for tests, but will also be used as a part of installation:

```
mkdir -pv /lib/udev/rules.d
mkdir -pv /etc/udev/rules.d
```

To test the results, issue:

```
make check
```

Install the package:

```
make install
```

Install some custom rules and support files useful in a PFS environment:

```
tar -xvf ../../udev-lfs-20171102.tar.xz
make -f udev-lfs-20171102/Makefile.lfs install
```

# 6.77.2. Configuring Eudev

Information about hardware devices is maintained in the /etc/udev/hwdb.d and /lib/udev/hwdb/ directories. Eudev needs information to be compiled into a binary database /etc/udev/hwdb.bin. Create the initial database:

```
udevadm hwdb --update
```

This command needs to be run each time the hardware information is updated.