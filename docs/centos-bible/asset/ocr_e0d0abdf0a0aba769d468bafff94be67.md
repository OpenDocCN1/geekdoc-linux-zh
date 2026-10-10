# ## Accessing and Running Applications



```
--> Processing Dependency: libgomp.so.1 for package: gcc
...
-->
Finished Dependency Resolution

Dependencies Resolved

==============================
Package Arch Version Repository Size
==============================
Installing:
gcc i386 4.1.2-42.el5 base 5.2 M
Installing for dependencies:
glibc-devel i386 2.5-24.el5_2.2 updates 2.0 M
glibc-headers i386 2.5-24.el5_2.2 updates 611 k
kernel-headers i386 2.6.18-92.1.22.el5 updates 854 k
libgomp i386 4.1.2-42.el5 base 82 k

Transaction Summary
==============================
Install 5 Package(s)
Update 0 Package(s)
Remove 0 Package(s)

Total download size: 8.7 M
Is this ok [y/N]: y
Downloading Packages
...
```

```
Running rpm_check_debug
Running Transaction Test
Finished Transaction Test
Transaction Test Succeeded
Running Transaction
Installing: libgomp ################################## [1/5]
Installing: kernel-headers ################################## [2/5]
Installing: glibc-headers ################################## [3/5]
Installing: glibc-devel ################################## [4/5]
Installing: gcc ################################## [5/5]

Installed: gcc.i386 0:4.1.2-42.el5
Dependency Installed: glibc-devel.i386 0:2.5-24.el5_2.2 kernel-headers.i386 0:2.6.18-92.1.22.el5 libgomp.i386 0:4.1.2-42.el5
Complete!
```