comes from Scientific Linux 6, as shown in Figure 7-7. While it includes a number of different repositories, you can learn from the pattern of directives configured for each repository.

There are four stanzas of data shown in Figure 7-7. Each stanza represents a connection to a Scientific Linux repository. For example, the first stanza includes the basic elements of a repository and more. The first line, in brackets, provides a name for the repository. In this case, the [sl] just happens to match the initials of Scientific Linux. It doesn't represent the directory where the associated packages are installed. That's a difference with the /etc/yum/pluginconf.d/rhnplugin.conf file described earlier.

[s1]

# FIGURE 7-7

Several repositories configured in one file

```
[sl]
name=Scientific Linux $releasever - $basearch
baseurl=http://ftp.scientificlinux.org/linux/scientific/$releasever/$basearch/os/
        http://ftp1.scientificlinux.org/linux/scientific/$releasever/$basearch/os/
        http://ftp2.scientificlinux.org/linux/scientific/$releasever/$basearch/os/
        http://ftp.scientificlinux.org/linux/scientific/mirrorlist/$releasever/$basearch/os/
#mirrorlist=http://ftp.scientificlinux.org/linux/scientific/mirrorlist/sl-base-6.txt
enabled=1
gpgcheck=1
gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-sl file:///etc/pki/rpm-gpg/RPM-GPG-KEY-dawson

[sl-testing]
name=Scientific Linux $releasever Testing - $basearch
baseurl=http://ftp.scientificlinux.org/linux/scientific/rolling/testing/$basearch/
        http://ftp1.scientificlinux.org/linux/scientific/rolling/testing/$basearch/
        http://ftp2.scientificlinux.org/linux/scientific/rolling/testing/$basearch/
        http://ftp.scientificlinux.org/linux/scientific/rolling/testing/$basearch/

enabled=0
gpgcheck=0
gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-sl file:///etc/pki/rpm-gpg/RPM-GPG-KEY-dawson

[sl-source]
name=Scientific Linux $releasever Alpha - Source
baseurl=http://ftp.scientificlinux.org/linux/scientific/$releasever/SRPMS/
        http://ftp1.scientificlinux.org/linux/scientific/$releasever/SRPMS/
        http://ftp2.scientificlinux.org/linux/scientific/$releasever/SRPMS/
        http://ftp.scientificlinux.org/linux/scientific/$releasever/SRPMS/

enabled=0
gpgcheck=1
gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-sl file:///etc/pki/rpm-gpg/RPM-GPG-KEY-dawson

[sl-testing-source]
name=Scientific Linux $releasever Testing - Source
baseurl=http://ftp.scientificlinux.org/linux/scientific/rolling/testing/SRPMS/
        http://ftp1.scientificlinux.org/linux/scientific/rolling/testing/SRPMS/
        http://ftp2.scientificlinux.org/linux/scientific/rolling/testing/SRPMS/
        http://ftp.scientificlinux.org/linux/scientific/rolling/testing/SRPMS/

enabled=0
gpgcheck=0
gpgkey=file:///etc/pki/rpm-gpg/RPM-GPG-KEY-sl file:///etc/pki/rpm-gpg/RPM-GPG-KEY-dawson
```