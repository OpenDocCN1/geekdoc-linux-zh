However, when you run the yum update command to update the local database of those remote packages, it includes sl as the name of the repository, in output similar to the following, which suggests that it took ten seconds to download the 1.6MB database of existing repository data.

```
sl | 1.6MB 00:10
```

While the name of the repository follows, it's just for documentation purposes and does not affect how packages or package databases are read or downloaded. However, the inclusion of the name directive does avoid a nonfatal error message.

```
name=Scientific Linux $releasever - $basearch
```

Note the several baseurl directives that follow. While only one is required, multiple baseurl directives specify the URL to different remote servers with the a copy of the actual repository of packages. It can work with either the HTTP or the FTP protocol. (It can even work with local directories or mounted Network File System shares, as described in Exercise 7-1.)

```
baseurl=http://ftp.scientificlinux.org/linux/scientific/$releasever/$basearch/os/
```

Alternatively, these repositories can be set up in a file downloaded with the mirrorlist directive:

```
#mirrorlist=http://ftp.scientificlinux.org/linux/scientific/mirrorlist/sl-base-6.txt
```

While repositories configured in .repo files in the /etc/yum.repos.d directory are enabled by default, the following directive provides an easy way to deactivate a connection to such (enabled=0 would deactivate the connection):

```
enabled=1
```

If you want yum to check the GPG signatures of each package to be downloaded, the following command puts that wish into effect:

```
gpgcheck=1
```

Of course, any GPG check requires a GPG key; the following directive specifies two keys from the local /etc/pki/rpm-gpg directory for that purpose:

```
gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-sl file:///etc/pki/rpm-gpg/RPM-GPG-KEY-dawson
```