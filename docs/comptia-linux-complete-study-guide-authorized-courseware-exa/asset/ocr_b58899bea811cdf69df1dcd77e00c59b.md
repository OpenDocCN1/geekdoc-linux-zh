+   5. Which of the following commands will extract the contents of the `myfonts.rpm` file into the current directory?
+       A. `rpm2cpio myfonts.rpm | cpio -i --make-directories`
+       B. `rpm2cpio myfonts.rpm > make-directories`
+       C. `rpm -e myfonts.rpm`
+       D. `alien --to-extract myfonts.rpm`

+   6. To use `dpkg` to remove a package called `theprogram`, including its configuration files, which of the following commands would you issue?
+       A. `dpkg -P theprogram`
+       B. `dpkg -p theprogram`
+       C. `dpkg -r theprogram`
+       D. `dpkg -r theprogram-1.2.3-4.deb`

+   7. Which of the following describes a difference between `apt-get` and `dpkg`?
+       A. `apt-get` provides a GUI interface to Debian package management; `dpkg` doesn't.
+       B. `apt-get` can install tarballs in addition to Debian packages; `dpkg` can't.
+       C. `apt-get` can automatically retrieve and update programs from Internet sites; `dpkg` can't.
+       D. `apt-get` is provided only with the original Debian distribution, but `dpkg` comes with Debian and its derivatives.

+   8. What command would you type to obtain a list of all installed packages on a Debian system?
+       A. `apt-cache pkgnames`
+       B. `apt-cache showpkg`
+       C. `dpkg -r allpkg`
+       D. `dpkg -i`

+   9. As *root*, you type `apt-get update` on a Debian system. What should be the effect of this command?
+       A. None; `update` is an invalid option to `apt-get`.
+       B. The APT utilities deliver information about the latest updates you've made to the APT Internet repositories, enabling you to share your changes with others.
+       C. The APT utilities download all available upgrades for your installed programs and install them on your system.
+       D. The APT utilities retrieve information about the latest packages available so that you may install them with subsequent `apt-get` commands.

+   10. Which of the following commands would you type to update the `unzip` program on a Fedora system to the latest version? (Select all that apply.)
+       A. `yum update unzip`
+       B. `yum upgrate unzip`
+       C. `yum -u unzip`
+       D. `yum -U unzip`