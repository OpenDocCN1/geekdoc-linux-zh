# 6.39. Inetutils-1.9.4

The Inetutils package contains programs for basic networking.
Approximate build time: 0.3 SBU
Required disk space: 29 MB

# 6.39.1. Installation of Inetutils

Prepare Inetutils for compilation:

```
./configure --prefix=/usr \
--localstatedir=/var \
--disable-logger \
--disable-whois \
--disable-rpc \
--disable-rexec \
--disable-rlogin \
--disable-rsh \
--disable-servers \
```

The meaning of the following options:

+   - --disable-logger
  This option prevents Inetutils from installing the logger program, which is used by scripts to pass messages to the System Log Daemon. Do not install it because Util-linux installs a more recent version.
- --disable-whois
  This option disables the building of the Inetutils whois client, which is out of date. Instructions for a better whois client are in the BLFS book.
- --disable-r*
  These parameters disable obsolete programs that should not be used due to security issues. The functions provided by these programs can be provided by the openssh package in the BLFS book.
- --disable-servers
  This disables the installation of the various network servers included as part of the Inetutils package. These servers are deemed inappropriate in a basic LFS system. Some are insecure by nature and are only considered safe on trusted networks. Note that better replacements are available for many of these servers.

Compile the package:

```
make
```

To test the results:

```
make check
```

> Note
One test, libls.sh, may fail in the initial chroot environment but will pass if the test is rerun after the LFS system is complete. One test, ping-localhost.sh, will fail if the host system does not have ipv6 capability.