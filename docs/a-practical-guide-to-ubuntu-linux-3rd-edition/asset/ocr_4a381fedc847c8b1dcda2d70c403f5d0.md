```
$ apt-cache rdepends nfs-common
nfs-common
Reverse Depends:
  rmanager
  nfs-kernel-server
  mount
  mount
  autofs5
```

**Displaying package records**   The `apt-cache show` command displays package records from the files in the APT local package indexes. See also the `aptitude show` command, which displays less information (page `529`), and the `dpkg status` command (page `537`). Following is an example:

```
$ apt-cache show nfs-common
Package: nfs-common
Priority: optional
Section: net
Installed-Size: 588
Maintainer: Ubuntu Developers <ubuntu-devel-discuss@lists.ubuntu.com>
Original-Maintainer: Anibal Monsalve Salazar <anibal@debian.org>
Architecture: i386
Source: nfs-utils
Version: 1.1.2.0-4ubuntu2
Replaces: mount (<< 2.13~), nfs-client, nfs-kernel-server (<< 1.1.0-7.5)
Provides: nfs-client
Depends: portmap (>= 6.0-10ubuntu1), adduser, ucf, lsb-base (>= 1.3-9ubuntu3), netbase (>= 4.24), initscripts (>= 2.86.0~ds1-3s), libc6 (>= 2.4), libcomerr2 (>= 1.0.1), libevend-1.4-2 (>= 1.4.13-stable), libgssapi-krb5-2 (>= 1.6.dfsg.2), libgssgluel, libk5crypto3 (>= 1.6.dfsg.2), libkrb5-3 (>= 1.6.dfsg.2), libnfsidmap2, librpcsecgss3, libwrap0 (>= 7.6.4~), upstart-job
Conflicts: nfs-client
Filename: pool/main/n/nfs-utils/nfs-common_1.1.2.0-4ubuntu2_i386.deb
Size: 211256
MD5sum: d047339007b36e2b931cc473e0b121d
SHA1: 4b2f71dcd330df3219a41539c59c5f7f5095213592b
SHA256: 653a684fcf75e5e676962ba3270fa0eb12a3f4b0ed5384cb024leb3824c93fa
Description: NFS support files common to client and server
Use this package on any machine that uses NFS, either as client or server. Programs included: lockd, statd, showmount, nfstatd, gssd and idmapd.

Upstream: SourceForge project "nfs", CVS module nfs-utils.
Homepage: http://nfs.sourceforge.net/
Bugs: https://bugs.launchpad.net/ubuntu/+filebug
Origin: Ubuntu
Supported: Sy
```

The `apt-cache showpkg` command displays package version and location information as well as dependency lists.