The “not a working copy” error means that any source code here can’t be used with Subversion.

The svnlite(1) command to grab source code looks like so.

```
# svnlite checkout \*svn.freebsd.org/@repository/@branch @locadir
```

The mirror ① is a FreeBSD Subversion mirror. The mirror svn.FreeBSD.org is a geo-routed alias for the closest subversion mirror.

The repository ② is the group of code you’re working with. You can get a complete list of current repositories at https://svnweb.FreeBSD.org/. The main Project repositories include base, for the operating system; doc, for documentation; and ports, for the Ports Collection.

The branch ③ is the version of FreeBSD you want. For the very latest stumpy-fingered current, use head. To get a stable version, use the branch stable/ followed by the major release. FreeBSD 12-stable would be stable/12. To get a release plus all current patches, use releng/ and the release number. The fully patched FreeBSD 12.2 would be at releng/12.2.

If you have trouble figuring out which branch you need, wander through https://svnweb.freebsd.org/. The branch literally tells svnlite(1) which subdirectory to grab from this site.

Finally, the locadir ④ is the local directory where I want to put the source code.

This host is running FreeBSD 11.1. I want to be adventuresome and move up to FreeBSD 11-stable. Here’s how I’d do that:

```
# svnlite checkout https://svn0.us-east.FreeBSD.org/base/stable/11 /usr/src/

Error validating server certificate for 'https://svn0.us-east.freebsd.org:443':
  - The certificate is not issued by a trusted authority. Use the
    fingerprint to validate the certificate manually!
Certificate information:
  - Hostname: svn0.freebsd.org
  - Valid: from Jul 29 22:01:21 2013 GMT until Dec 13 22:01:21 2040 GMT
  - Issuer: svn0.freebsd.org, clusteradm, FreeBSD.org, CA,
    US(clusteradm@freebsd.org)
  - Fingerprint: 1C:BD:85:95:11:9F:EB:75:A5:4B:C8:A3:FE:08:E4:02:73:06:1E:61
(R)eject, accept (t)emporarily or accept (p)ermanently? p
```