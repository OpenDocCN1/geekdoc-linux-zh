```
/usr/sbin/amflush
/usr/sbin/amlabel
/usr/sbin/amrestore
/usr/sbin/amtape
%dir /usr/lib/amanda/
/usr/lib/amanda/taper
/usr/lib/amanda/dumper
/usr/lib/amanda/driver
/usr/lib/amanda/planner
/usr/lib/amanda/reporter
/usr/lib/amanda/getconf
/usr/lib/amanda/chg-generic
/usr/man/man8/amanda.8
/usr/man/man8/amadmin.8
/usr/man/man8/amcheck.8
/usr/man/man8/amcleanup.8
/usr/man/man8/amdump.8
/usr/man/man8/amflush.8
/usr/man/man8/amlable.8
/usr/man/man8/amrestore.8
/usr/man/man8/amtape.8
%doc README
%doc COPYRIGHT
%doc docs/INSTALL
%doc docs/KEBEROS
%doc docs/SUNOS4.BUG
%doc docs/SYSTEM.NOTES
%doc docs/TAPE.CHANGERS
%doc docs/WHATS.NEW
%doc docs/MULTITAPE
%doc example
```

You’ll note that we neglected to use the%doc directive on the man page files. The reason is that RPM automatically tags any file destined for /usr/man as documentation. Now our spec file has a complete set of tags, the two subpackages are defined, it has build-time scripts that work, and, now, %files lists for each subpackage. Why don’t we try that build again?

```
# rpm -ba amanda-2.3.0.spec
* Package: amanda
* Package: amanda-client
* Package: amanda-server
...
echo Executing: %build
Executing: %build
+ cd /usr/src/redhat/BUILD
+ cd amanda-2.3.0
+ make
Making all in common-src
...
+ echo Executing: %install
Executing: %install
+ cd /usr/src/redhat/BUILD
+ cd amanda-2.3.0
+ make install
Making install in common-src
...
+ echo Executing: special doc
Executing: special doc
```