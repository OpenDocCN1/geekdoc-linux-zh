```
Fetching 10697 patches....10....20....30....40....50....60....70....80....90
```

Go make a cup of tea. Depending on your host's bandwidth, you should return to see:

```
Applying patches...
```

You tea's probably too hot. Let it cool a bit.

```
Fetching 236 files...
```

More downloading? Fine, enjoy your tea and watch the program work.

```
Attempting to automatically merge changes in files... done.
The following files will be removed as part of updating to 11.1-RELEASE-p1:
/usr/include/c++/v1/__undef__deallocate
/usr/include/c++/v1/tr1/__undef__deallocate
/usr/include/netinet/ip_ipsec.h
--snip--
```

You can search the mailing list archives and the FreeBSD source code tree to learn why each of these files was removed.

The minor release will include new features backported from -current. Those probably involve adding files to the system.

```
The following files will be added as part of updating to 11.1-RELEASE-p1:
/boot/kernel/amd_ecc_inject.ko
/boot/kernel/bytgpio.ko
/boot/kernel/cfiscsi.ko
/boot/kernel/cfunass.ko
--snip--
```

None of these new features should interfere with existing functions, but perusing the list might give you some interesting reading.

An upgrade should change just about every file on the system, as we'll see next.

```
The following files will be updated as part of updating to 11.1-RELEASE-p1:
/.cshrc
/.profile
/COPYRIGHT
/bin/[
```