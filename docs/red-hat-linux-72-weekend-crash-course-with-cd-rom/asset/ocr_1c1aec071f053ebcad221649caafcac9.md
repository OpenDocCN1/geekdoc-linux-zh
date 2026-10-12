Whenever possible, you should use `rpm -U` to upgrade software, rather than doing it manually yourself by removing the old package (`rpm -e`) and then installing the new version (using `rpm -i`). Why? Allowing RPM to perform the upgrade using `rpm -U` automatically saves the old configuration files, which saves you the hassle of configuring the software after a fresh installation. If you manually type `rpm -e` followed by `rpm -i` to erase an old RPM and install its replacement, the erase operation *also* deletes the old configuration files. The `rpm` upgrade command contains logic to save the old configuration files.

![](bbox=[0.13, 0.25, 0.22, 0.34])

> When you upgrade the kernel and the kernel module packages that contain a ready-to-run Linux kernel, do not use the `rpm -U` command. Instead, install it with the `rpm -i` command. Using `rpm -i` ensures that you don't overwrite files being used by the current kernel.

# Verifying RPMs with the `rpm` command

You may not do this often, but if you suspect that a software package is not properly installed, use the `rpm -V` command to verify the package. For example, to verify the kernel package, type the following:

```
rpm -V kernel

```

This causes `rpm` to compare size and other attributes of each file in the package against the original files. If everything verifies correctly, the `rpm -V` command does not print anything. If it detects any discrepancies, `rpm` displays a report of the discrepancies. For example, suppose you modified the configuration files for the Apache Web server. Here is what you might see when you verified the Apache package:

```
rpm -V apache
S,5....T c /etc/httpd/conf/httpd.conf

```

In this case, the output from `rpm -V` shows that a configuration file has changed. Each line of this command's output consists of three parts:

+   * The line starts with eight characters; each character indicates the type of discrepancy found. For example, S means the size has changed since the file was originally installed. T means the last modification time has changed. A period (.) indicates that a specific attribute matches the original.
+   * For configuration files, an `c` appears next; otherwise, this field is blank. That's how you can tell whether a file is a configuration file. Typically, you don't have to worry if a configuration file has changed because you probably made the changes yourself.
+   * The last part of the line is the file's full pathname. From this part, you can tell the exact location of the file.