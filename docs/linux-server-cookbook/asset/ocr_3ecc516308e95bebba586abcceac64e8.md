```
```
root@ubuntu:~# dpkg -L pci.ids
/.
/usr
/usr/share
/usr/share/doc
/usr/share/doc/pci.ids
/usr/share/doc/pci.ids/changelog.Debian.gz
/usr/share/doc/pci.ids/copyright
/usr/share/misc
/usr/share/misc/pci.ids
```
```

*Figure 4.41: Output example listing the files created by a specific package.*

+   3. List from all packages installed in the system, as shown in *figure 4.42*: 

```
```
root@ubuntu:~# dpkg -l
Desired=Unknown/Install/Remove/Purge/Hold
| Status=Not/Inst/Conf-files/Unpacked/halF-conf/Half-inst/trig-aWait/Trig-pend
||/ Err?(none)/Reinst-required (Status,Err: uppercase=bad)
||/ Name Version Architecture
+++-========================-================-==============-===============
ii adduser 3.118ubuntu5 all
ii amd64-microcode 3.20191218.1ubuntu2 amd64
ii apparmor 3.0.4-2ubuntu2 amd64
ii apport 2.20.11-0ubuntu82.1 all
ii apport-symptoms 0.20 all
ii apt 2.4.5 amd64
ii apt-utils 2.4.5 amd64
ii base-files 12ubuntu4 amd64
ii base-passwd 3.5.52build4 amd64
ii bash 5.1-6ubuntu1 amd64
ii bash-completion 1:2.11-5ubuntu1 all
```
```

*Figure 4.42: Output example listing the packages installed in the system.*

+   4. Filter the list of the packages installed using a pattern, as shown in *figure 4.43*: 

```
```
root@ubuntu:~# dpkg -l "distro-info*"
Desired=Unknown/Install/Remove/Purge/Hold
| Status=Not/Inst/Conf-files/Unpacked/halF-conf/Half-inst/trig-aWait/Trig-pend
||/ Err?=none/Reinst-required (Status,Err: uppercase=bad)
||/ Name Version Architecture Description
+++==================-===============-====================================
ii distro-info 1.1build1 amd64 provides information about the distributions
ii distro-info-data 0.52ubuntu0.1 all information about the distributions' release
lines 1-7/7 (END)
```
```

*Figure 4.43: Output example filtering the list of packages installed in the system.*

+   5. Search what installed packages created the file `/etc/sudo.conf`, as shown in *figure 4.44*: