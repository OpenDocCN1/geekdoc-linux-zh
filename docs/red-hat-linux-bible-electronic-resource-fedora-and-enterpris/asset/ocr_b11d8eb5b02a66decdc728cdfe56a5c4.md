```
# rpm -qc ppp
/etc/pam.d/ppp
/etc/ppp/chap-secrets
/etc/ppp/options
/etc/ppp/pap-secrets
```

If you ever want to know which package a particular command or configuration file came from, you can use the `-qf` option. In the following example, the -qf option displays the fact that the chgrp command comes from the fileutils package:

```
# rpm -qf /bin/chgrp
fileutils-4.1-4
```

# Verifying packages with rpm

If something in a software package isn't working properly, or if you suspect that your system has been tampered with, the verify (-V) option of rpm can help you verify installed software against its original software package. Information about each installed package is stored on your computer in the RPM database. By using the verify option, you can check whether any changes were made to the components in the package.

> NOTE: The verify option uses the uppercase letter (-V), while the verbose option uses the lowercase (-v).

Various file size and permissions tests are done during a verify operation. If everything is fine, there is no output. Any components that have changed from when they were installed will be printed along with information indicating how they were changed. Here's an example:

```
# rpm -V ppp
S.5...T c /etc/ppp/chap-secrets
S.5...T c /etc/ppp/options
S.5...T c /etc/ppp/pap-secrets
```

This output shows that the ppp package (used to dial-up a TCP/IP network such as the Internet) has had three files changed since it was installed. The notation at the beginning shows that the file size (S), the MD5 sum (5), and the modification time (T) have all changed. The letter c shows that these are all configuration files. By reviewing these files to see that the changes were only those that I made to get PPP working, I can verify that the software is okay.

The indicators that you may see when you verify the contents of a configuration file are:

+   - 5 — MD5 Sum — An MD5 checksum indicates a change to the file contents.

+   - S — File size — The number of characters in the file has changed.

+   - L — Symlink — The file has become a symbolic link to another file.

+   - T — Mtime — The modification time of the file has changed.

+   - D — Device — The file has become a device special file.