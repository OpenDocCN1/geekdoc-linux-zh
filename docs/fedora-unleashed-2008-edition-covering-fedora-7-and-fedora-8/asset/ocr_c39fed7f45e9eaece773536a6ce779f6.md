Remember that `RPM` was created not only to provide an easy-to-use administrative tool, but also as a developer’s tool for use in multiplatform source-code package management. Programmers using `rpm` for development and distribution use its `rpm` build command, along with a myriad of additional command-line flags. `RPM` can be used to build binaries, execute programs, test installations, verify and sign packages, build source packages, track versions, and target builds for specific architectures. You can find details at the `RPM` home page (http://www.rpm.org).

# Using rpm on the Command Line

Although several `GUI` clients make use of `rpm`, you can perform all five basic `rpm` operations by using the `rpm` command from the command line. This section gives you an introduction to performing those operations. It also provides examples of how to install, verify, query, remove, and upgrade a software package.

The most common `rpm` operation is software installation. Using `rpm` is an easy way to keep track of installed software, and it can be used to quickly remove undesired packages. Use the `-i` option, along with the full or partial name (using regular expressions) of a software package, to install software with `rpm`. For example, to install the `RPM` file for configuring the usage of the `FreshRPMs` repository, use the `rpm` command like this:

```
# rpm -ivh http://ftp.freshrpms.net/pub/freshrpms/fedora/linux/ \
# /freshrpms-release/freshrpms-release-1.1-1.fc-noarch.rpm
Retrieving http://ftp.freshrpms.net/pub/freshrpms/fedora/linux/ \
# /freshrpms-release/freshrpms-release-1.1-1.fc-noarch.rpm
warning: /var/tmp/rpm-xfer.48amVs: V3 DSA signature: NOKEY, key ID 8df56d05
Preparing...   ##################################################### [100%]
1:freshrpms-release   ##################################################### [100%]
```

This example uses the `v` and `h` options, which provide a more verbose output and display of hash marks to show the progress of the installation. The example also demonstrates the capability of `rpm` to use `HTTP` or `FTP` servers to fetch files for installation. It also shows that `rpm` can use `GPG` keys to validate a file. (The key was not installed in the example.)

You can also use `rpm` to query its database after installing packages to verify an installation. Use the `-q` option, along with the name of a software package, to verify installation of your system. For example, to verify the `freshrpms-release` package, use the `rpm` command like this:

```
# rpm -V freshrpms-release
```