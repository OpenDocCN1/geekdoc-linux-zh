# Kernel Versions

Each new kver has an associated kernel source RPM and it is installed with

```
# rpm -Uvh newkernel.src.rpm
```

The source code is automatically installed to /usr/src.

# Kernel Versions

The Linux kernel is in a constant state of development. As new features are added, bugs are fixed, and new technology is incorporated into the code base, it becomes necessary to provide stable releases of the kernel for use in a production environment. It's also important to have separate releases that contain the newest code for developers to test. To keep track of the kernels, version numbers that have abstract meaning. Is version 8 twice as advanced as version 4 of the same application? Is version 1 of one less developed than version 3 of another? The version numbers can't be used for this kind of qualitative or quantitative comparison. It's entirely possible that higher version numbers have fewer features and more bugs than older versions. The numbers exists solely to differentiate and organize sequential revisions of software.

On the authors' test system, for example, the kernel version number is 2.4.19-7.80.

The kernel version can be broken down into four sections:

+   * major version—This is the major version number, now at 2. Think of this as volume 2 of a book.
* minor version—This is the minor version number, now at 4. Think of this as Chapter 4 in volume 2 of that book.
* sublevel number—This indicates the current iteration of the kernel; for our preceding example, it is at 19. Think of this as page 19 of Chapter 4, volume 2 in that book.
* extraversion level—This is the number representing a collection of patches and additions made to the kernel by the Red Hat engineers to make the kernel work for them (and you). Each collection is numbered, and the number is indicated here in the kernel name. From our preceding example, it is 7.80. Think of this as the 7.8th revision of page 19, Chapter 4, volume 2 in that book.

Typing uname -r at the command prompt displays your current kernel version.

```
# uname -r
2.4.18-7.80
```