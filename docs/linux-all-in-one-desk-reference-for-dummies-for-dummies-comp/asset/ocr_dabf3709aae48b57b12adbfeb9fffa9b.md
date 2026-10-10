Table 4-1 Characters Used in RPM Verification Reports
| Character | Meaning |
| S | Size has changed |
| M | Permissions and file type are different |
| 5 | Checksum computed with the MD5 algorithm is different |
| D | Device type is different |
| L | Symbolic link is different |
| U | File's user is different |
| G | File's group is different |
| T | File's modification time is different

# Working with DEB Files

Debian packages with `.deb` file extensions store executable files together with configuration files, online documentation, and other information. You can unpack and manipulate these DEB files using the Debian utility `dpkg`, which is a command-line program that takes many options. A text mode, menu-driven program called dselect is also available for you to manage the packages without having to type `dpkg` commands.

You typically use a higher-level utility called APT (Advanced Packaging Tool) to work with packages in Debian. For example, instead of downloading a DEB file and installing it with the `dpkg` command, you can simply use the `apt-get` command to install the package. The `apt-get` command can even download the package from an online Debian repository and install it on your system. The `dpkg` command is still useful when you want to look at the contents of a DEB file that you have manually downloaded from a repository or that might be in the APT cache directory (`/var/cache/apt/archives` in Debian).

![](bbox=[0.16, 0.55, 0.21, 0.61])

I introduce you to `dpkg`, `dselect`, and APT in the following sections.

# Understanding DEB filenames

A typical DEB package has a filename of the following form:

```
mozilla-firefox_1.0.2-1_i386.deb
```

The filename has three parts separated by underscores (_):