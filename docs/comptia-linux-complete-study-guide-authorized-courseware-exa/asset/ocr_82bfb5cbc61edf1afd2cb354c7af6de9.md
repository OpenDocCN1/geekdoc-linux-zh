# Review Questions

+   1. Which of the following is not an advantage of a source package over a binary package?
+      A. A single source package can be used on multiple CPU architectures.
+      B. By recompiling a source package, you can sometimes work around library incompatibilities.
+      C. You can modify the code in a source package, altering the behavior of a program.
+      D. Source packages can be installed more quickly than binary packages can.

+   2. Which is true of using both RPM and Debian package management systems on one computer?
+      A. It’s generally inadvisable because the two systems don’t share installed-file database information.
+      B. It’s impossible because their installed-file databases conflict with one another.
+      C. It causes no problems if you install important libraries once in each format.
+      D. It’s a common practice on Red Hat and Debian systems.

+   3. Which of the following statements is true about binary RPM packages that are built for a particular distribution?
+      A. They can often be used on another RPM-based distribution for the same CPU architecture, but this isn’t guaranteed.
+      B. They may be used in another RPM-based distribution only when you set the --convert-distrib parameter to rpm.
+      C. They may be used in another RPM-based distribution only after you convert the package with alien.
+      D. They can be recompiled for an RPM-based distribution running on another type of CPU.

+   4. An administrator types the following command on an RPM-based Linux distribution:
+      # rpm -ivh megaprog.rpm
+      What is the effect of this command?
+      A. The megaprog package, if it’s installed, is uninstalled from the computer.
+      B. The megaprog.rpm package, if it exists, is valid, and isn’t already installed, is installed on the system.
+      C. The megaprog.rpm source RPM package is compiled into a binary RPM for the computer.
+      D. Nothing; megaprog.rpm isn’t a valid RPM filename, so rpm will refuse to operate on this file.