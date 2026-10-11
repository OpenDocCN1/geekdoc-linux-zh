# Example 10-3 Sample make linux Output (Continued)

```
cc -DFACILITY=LOG_MAIL -DHOSTS_ACCESS -DPARANOID -DOPTPEERNAME_BUG -
DBROKEN_POSIX -DLIBC_CLIBS_STROKTS -DDARWIN_UNAS=-022 -DBREAL_DARWIN_DIR='/usr/
sbin' -DSBYSVINT=LOG_T1000 -DRFRC_991_TIMPOTET=-10 -DHOSTS_DENY='/etc/hosts.deny'
-DHOSTS_ALLOW='/etc/hosts.allow' -DBROKEN_SO_LINGER -DSYS_SREJLIST_DEFINED -
-Dvysblog=mysyslog -DALLWAYS_HOSTNAME -ctcp_dckptd tcpdchk.o fakelog.o inetcf.o
scalfold.o libwrap.a
make[1]: Leaving directory '/usr/src/tcp_wrappers'
```

Now, to install the software, follow the steps outlined in Example 10-4. If
you wish to use alternate directories (such as /usr/local/sbin instead of /usr/
sbin, for example) or different permission settings, feel free to modify these
steps accordingly. Also, note that the first step incorporates `mkdir -p`, which
will not be necessary if the indicated directories already exist. If you execute it
anyway, it will benignly report its inability to create directories that already
exist. Note that the strip operation on the executable images removes the
symbols therefor, providing modest performance and security enhancements.

# Example 10-4 Installing TCP_Wrappers

```
#mkdir -p /usr/{include,lib,man/man3,man/man5,man/man8,sbin}
#cp hosts_access.3 /usr/man/man3
#cp hosts_access.5 /usr/man/man5
#cp tcpd.8 tcpdchk.8 tcpdmatch.8 /usr/man/man8
#if -f hosts_access.5 /usr/man/man5/hosts.allow.5
#if -f hosts_access.5 /usr/man/man5/hosts.deny.5
#cp libwrap.a /usr/lib
#cp tcpd.h /usr/include
#install -m755 safe_finger /usr/sbin
#install -m755 tcpd /usr/sbin
#install -m755 tcpdchk /usr/sbin
#install -m755 tcpdmatch /usr/sbin
#install -m755 try-from /usr/sbin
#strip /usr/sbin/tcpd /usr/sbin/tcpdchk
#strip /usr/sbin/tcpdmatch /usr/sbin/safe_finger
#strip /usr/sbin/try-from
```

Optionally, you may also wish to copy the additional files

```
BLURB CHANGES README DISCLAIMER Banners Makefile
```

to a standard resource directory. On Red Hat 5.2/6.0, this is normally /usr/
doc/tcp_wrappers-7.6.

Finally, you may clean the source tree (remove all generated object and
binary files) by executing `make clean`, as displayed in Example 10-5.

# Example 10-5 Cleaning Up after Installation

```
# make clean
rm -f tcpd miscd safe_finger tcpdmatch tcpdchk try-from *. [oa] core \
.cflags
#
```

This completes the compilation and installation! Let's go on and see how
TCP_wrappers works.