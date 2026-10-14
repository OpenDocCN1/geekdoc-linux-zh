The option -f only works if you specify the complete filename with a full path. You can enter several filenames, as in the following:

```
```text
da10:~ # rpm -qf /bin/rpm /usr/bin/wget
rpm-4.4.2-43
wget-1.10.2-15
```
```

This returns information for both /bin/rpm and /usr/bin/wget. With the help of the RPM database, you can perform verification checks with the option -V, or --verify. If any files in a package have been changed since installation, they will be displayed.

RPM uses the character symbols shown in Table 6-2 to provide hints about the changes.

| Character | Description |
|---|---|
| 5 | MD5 check sum |
| S | File size |
| L | Symbolic link |
| T | Modification time |
| D | Major and minor device numbers |
| U | Owner |
| G | Group |
| M | Mode (permissions and file type) |

Table 6-2

In the case of configuration files, the letter c is displayed. The following is an example for changes to /etc/wgetrc (wget):

```
```text
rpm -V wgetS.5.....T c /etc/wgetrc
```
```

# Install, Update, and Uninstall Packages

For most RPM packages, you use the following command to install the software:

```
```text
rpm --i *package_name*.rpm
```
```

When you install an RPM package, the executable programs, documentation files, configuration files, and start scripts are copied to the appropriate directories in the file system.

You can use the options -U (or --upgrade) and -F (or --freshen) to update a package by using the following syntax:

```
```text
rpm --F *package_name*.rpm
```
```

This command removes the files of the old version and immediately installs the new files. If no previous version is installed, the package is not installed.