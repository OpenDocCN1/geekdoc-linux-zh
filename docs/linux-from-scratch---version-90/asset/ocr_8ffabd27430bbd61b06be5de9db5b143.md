# Linux From Scratch - Version 9.0

In some systems, /dev/shm is a symbolic link to /run/shm. The /tmpfs was mounted above so in this case only a directory needs to be created.

```
if -h $LFS/dev/shm; then
mkdir -pv $LFS/$($LFS/dev/readlink)
fi
```

# 6.3. Package Management

Some reasons why package management is mentioned in LFS or BLFS:

+   * Dealing with package management takes the focus away from the goals of these books—teaching a Linux system is built.

+   * There are multiple solutions for package management, each having its strengths and drawbacks. One that satisfies all is difficult.

There are some hints written on the topic of package management. Visit the Hints Project and see if one of them fits your need.

# 6.3.1. Upgrade Issues

+   * If Glibc needs to be upgraded to a newer version (e.g. from glibc-2.19 to glibc-2.20), it is safer to rebuild LFS. You may have to rebuild all the packages in their dependency order, or we do not recommend it.

+   * If a package contains a shared library is updated, and if one of the library changes, then all the packages dynamically linked to the library need to be recompiled against the new library. (Note that there is no correlation between the package name and the name of the library). For example, a package foo installs a shared library with name libfoo.so.1. Say you upgrade the package to a newer version foo-1.2.4 that installs a shared library with name libfoo.so.2. In this case, all packages that are dynamically linked to libfoo.so.1 need to be recompiled to link against libfoo.so.2. Note that you should not remove the previous libraries unless the dependent packages are recompiled.

# 6.3.2. Package Management Techniques

The following are some common package management techniques. Before making a decision on a package manager, do some research on the various techniques, particularly the drawbacks of the particular scheme.

# 6.3.2.1. It is All in My Head

Yes, this is a package management technique. Some folks do not find the need for a package manager because they know the packages intimately and know what files are installed by each package. Some users also do not need any package management because they plan on rebuilding the entire system when a package is changed.

81