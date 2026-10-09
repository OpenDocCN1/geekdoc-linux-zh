# 12.2 Setting Up the Sample Implementation

# 12.2.1 Sample Implementation Using chroot (1)

The chroot LSB-si is distributed as a compressed tarball that should simply be unpacked by the supereuser (Example 12.1). Later, other pieces can be layered on top of it, and packages for additional functionality can be installed inside it. For illustrative purposes, the IA32 (x86) architecture will be used in the following examples. For your situation, you may need to substitute the appropriate LSB architecture and version.

```
**Example 12.1: Installing LSB-si on IA32 (x86) Architecture**
```
# mkdir /opt/lsbsi-ia32
# cd /opt
# tar jxvf /tmp/lsbsi-ia32-2.0.1.tar.bz2
```
```

The LSB-si can be started by running the `/sbin/chroot` command (Example 12.2; some distributions place this command in `/usr/sbin`).

```
**Example 12.2: Starting LSB-si by the /sbin/chroot Command**
```
# /sbin/chroot /opt/lsbsi-ia32
```
```

To simulate a login session, use this command as shown in Example 12.3.

```
**Example 12.3: Login Session**
```
# /sbin/chroot /opt/lsbsi-ia32 /bin/hash -l
```
```

When working in the chroot, only files inside the chroot tree will be accessible. Since this limits the usefulness of the environment, some steps should be taken ahead of time to make the necessary files available. One approach is to simply copy files from the chroot into a suitable location. If another window or terminal session is available on the host system, it is also possible to copy files into the chroot tree the same way, whenever they are needed (Example 12.4).