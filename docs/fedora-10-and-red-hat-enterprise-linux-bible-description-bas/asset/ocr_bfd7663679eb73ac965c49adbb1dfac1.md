# 204 Part II: Using Fedora RHEL

+   - **nodops** Skips dependency checks and installs the package, even if packages it are not installed. This option should be used with extreme caution! By not resolving dependencies, you can end up with broken software.

+   - **--ignore** Forces package to be installed, even if the binaries in the package don't match the architecture of your host computer.

+   - **--excludedocs** Excludes any package members, infotext, or other files marked as documentation.

+   - **--ignoreos** Forces package to be installed, even if the binaries in the package don't match the architecture of your operating system.

The following is a simple command used to install an RPM package:

```
# rpm -U AdobeReader_enu-7.0.9-1.i386.rpm
```

I like to see feedback when I install something (by default, rpm is surprisingly quiet when it succeeds). Here is what the command looks like when I add the -vy option to get verbose feedback, along with some of the output:

```
# rpm -Uv AdobeReader_enu-8.1.3-1.i486.rpm
=============================================
D: AdobeReader_enu-8.1.3-1.i486.rpm
D: Expected size: 494981060 Iad96vs+agt(180)+pad(4)+data(49472806)
D: Actual size: 494981060
D: loading keys from /var/lib/rpm/pubkeys/*
D: couldn't find any keys in /var/lib/rpm/pubkeys/*
D: loading keys from rpmsdb
D: opening db /var/lib/rpm/Packages dbcl:spool:join
D: opening db index /var/lib/rpm/Packages rdnly node mode=0x0
D: locked db index /var/lib/rpm/Packages
D: opening db index /var/lib/rpm/sams rdnly node mode=0x0
D: read head #963 Header sanity check: OK
D: added key gpg-pubkey-4befc273-48b5df3 to keyring
D: Using legacy gpg-pubkey(s) from rpmsdb
D: AdobeReader_enu-8.1.3-1.i486.rpm. Header SHA1 digest: OK
(5cfaf2bdc5852735d38ffaa981dce0b1971f791)
D: read head #1489 Header SHA1 digest: OK (5cfaf2bdc5852735d38ffaa981dce0b1971f791)
D: added binary package [1]
D: found 0 source 1 binary packages
```

From this output, you can see that rpm finds one binary package in this archive, verifies the checksum, opens the RPM database, installs the packages, and checks the database when done. Another way to verify that the install is actually working is to add the -h option, as follows:

```
# rpm -Uvh AdobeReader_enu-8.1.3-1.i486.rpm
Preparing... #######################################
AdobeReader_enu ############################
```