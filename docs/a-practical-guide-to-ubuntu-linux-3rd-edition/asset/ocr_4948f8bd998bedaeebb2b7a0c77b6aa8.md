# # deb FILES

The **dpkg** management system works with **.deb** format files, frequently referred to as **deb** files. Because **dpkg** cannot download **deb** files from repositories, **aptitude** (page 526) typically performs this task. By default, **aptitude** stores downloaded **deb** files in `/var/cache/apt/archives`. The **dpkg** management system stores available package information in `/var/lib/dpkg/available` and package installation information in `/var/lib/dpkg/status`.

You can manually locate, download, and install **deb** files. However, doing so can be tedious, especially when you find that a package is dependent on several other packages and that some of those packages are dependent on yet other packages.

You can create **deb** files, as when you build a kernel. Page 579 has an example of building a kernel **deb** file; pages 536 and 582 show **dpkg** installing **deb** files.

Binary files  A binary **deb** file can contain the following components, which are packed and unpacked using the **ar** (archive) utility. All packages contain an executable file; the other components are optional.

+   *   **binary**—Binary executable files
+   *   **control**—Package information including lists of dependent, recommended, and suggested packages
+   *   **conffiles**—Package configuration files
+   *   **preinst**—Preinstall script
+   *   **postinst**—Postinstall script
+   *   **prerm**—Preremove script
+   *   **postrm**—Posteremove script

To unpack a **deb** file, first download it to `/var/cache/apt/archives` using the command **aptitude download package**. Copy the file to a directory with no other files in it and use **ar -xv** to unpack the **deb** file. You can then use **tar** (page 176) to unpack the tar files. The example shows how to extract the control files from the **nfs-common** **deb** file.

```
```
$ ls nfs-common.deb
nfs-common_1%3a1.2.0-4ubuntu2_i386.deb
$ sudo ar -xv nfs-common.deb
x - debian-binary
x - control.tar.gz
x - data.tar.gz
$ sudo tar -xvf control.tar.gz
./
./postinst
./preinst
./prerm
./postrm
./conffiles
./md5sums
./control
```
```