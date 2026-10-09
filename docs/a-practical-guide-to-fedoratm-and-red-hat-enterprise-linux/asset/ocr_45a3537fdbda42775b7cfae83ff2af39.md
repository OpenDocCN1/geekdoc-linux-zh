```
$ su -C 'yum-builddep --sam/kernel-3.9.8-300.fc19.src.rpm'
Password:
Loaded plugins: langpacks, refresh-packagekit
Getting requirements for kernel-3.9.8-300.fc19.src
...
Install  15 Packages (+37 Dependent packages)

Total download size: 36 M
Installed size: 108 M
Is this ok [y/d/N]: y
...
Complete!
```

Finally, working from your home directory as a nonprivileged user, use `rpm` to install the kernel source code in the `rpmbuild` directory hierarchy in your home directory:

```
$ rpm -Uvh kernel-3.9.8-300.fc19.src.rpm
  1:kernel    warning: user mockbuild does not exist -- using root
warning: group mockbuild does not exist -- using root
warning: user mockbuild does not exist -- using root
...
  1:kernel-3.9.8-300.fc19   ##################################################  [100%]
```

You can ignore errors, such as those shown above, about groups and users that do not exist.

# Preparing the Source Code

The final step before you can work with the source code is to prep it. Prepping unpacks compressed files and applies patches. The following `rpmbuild` command uses the `-bp` option to prep the source code:

```
$ cd /home/sam/rpmbuild/SPECS
$ rpmbuild -bp --target {arch} kernel.spec
Building target platforms: x86_64
Building for target x86_64
Executing(%prep): /bin/sh -e /var/tmp/rpm-tmp.qGVQ0c
+ umask 022
+ cd /home/sam/rpmbuild/BUILD
...
```

If `rpmbuild` cannot find a package it needs to prep the code, it displays a message such as the following:

```
error: Failed build dependencies:
  elfutils-libelf-devel is needed by kernel-3.9.8-300.fc19.x86_64
  zlib-devel is needed by kernel-3.9.8-300.fc19.x86_64
  binutils-devel is needed by kernel-3.9.8-300.fc19.x86_64
```

In this case, install the needed packages (you might have to install different packages than those in the example):

```
$ su -C 'yum install elfutils-libelf-devel zlib-devel binutils-devel'
```

After you install the packages, give the preceding `rpmbuild` command again. With the kernel source code installed and prepped on the local system, you can configure, compile, and install it.