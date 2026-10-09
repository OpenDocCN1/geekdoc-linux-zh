Example 13.13: Running configure without IPv6

```
```
$ ./configure --disable-ipv6
configure: Configuring rsync 2.5.5
...
$ make
....
lsbccc -g -02 -DHAVE_CONFIG_H -Wall -W -0 rsync rsvnc.o \
generator.o receiver.o cleanup.o sender.o exclude.o util.o \
main.o checksum.o match.o syscall.o log.o backup.o options.o \
flist.o iio.o compat.o hlink.o token.o udidlist.o socket.o \
fileio.o batch.o clientname.o params.o loadparm.o \
clientserver.o access.o connection.o authenticate.o \
lib/fmtmatch.o lib/compat.o lib/snprintf.o lib/mdfour.o \
lib/pfstring.o zlib/deflate.o zlib/inblock.o zlib/infcodes.o \
zlib/infast.o zlib/inflate.o zlib/inftrees.o zlib/inftil.o \
zlib/trees.o zlib/zutil.o zlib/adler32.o -ipopt -iresolv
authenticate.c:278: undefined reference to `auth_client':
```

    authenticate.c:278: undefined reference to `getpass'
    collect2: ld returned 1 exit status
    make: *** [rsync] Error 1
```

# ### 13.5.2 Checking the Binary

The lsbppchk can be used to statically check a binary for LSB compliance (Example 13.14). The static application checker examines an application to check that it is using only the libraries, interfaces, and runtime loader specified by the LSB, as well as to verify that its program image has some features required by the ELF format.

Example 13.14: Running the Application Checker

```
$ lsbppchk rsync
lsbppchk for LSB Specification 2.0.0
Checking binary rsync
$ 
```

If any problems are found, they will be output to standard error and recorded in a journal file named journal.binary_name.