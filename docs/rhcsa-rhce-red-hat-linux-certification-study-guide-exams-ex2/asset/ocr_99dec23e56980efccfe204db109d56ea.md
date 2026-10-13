![](bbox=[0.1, 0.18, 0.22, 0.32])

code archive. Such archives can be created and unpacked with the help of the tar command.

# Source code can also be compressed using the bzip2 algorithm.

To create an RPM, you're going to have to set up a similar archive in the same rpmbuild/SOURCES subdirectory. Once configured, you'll also have to create a . spec file, to be stored in the rpmbuild/SPECS subdirectory. You'll then be able to compile that package with the rpmbuild command.

# Install and Analyze the rpmbuild Command

The rpmbuild command is used to build a binary RPM from source code, as configured with a .spec file. As the command is not available by default, you'll have to install it from the rpm-build package. You should also install the rpmdevtools package, which will be useful shortly. To speed up the process, it's more efficient to use administrative privileges to use the yum command to install all of these packages, using the procedures described in Chapter 7.

```
# yum install rpm-build rpmdevtools
```

In general, if you want more information on how it works, run the rpmbuild command with the -v or -vv switch. Most documentation assumes the rpmbuild command uses a spec file in the rpmbuild/SPECS directory. In that case, you'd use the -b switch. Options with the -t switch are associated with a spec file included in the actual source-code archive in .tar or compressed .tar.gz format. Given current documentation, it's assumed that you'll configure a separate .spec file and would therefore use one of the -b switches described in Table 12-2.

TABLE 12-2
Switches for the rpmbuild Command

| Switch | Description |
|---|---|
| -ba | Builds both binary and source RPM packages. |
| -bb | Builds the binary RPM package. |
| -bc | Executes the %prep and %build commands from the .spec file. |
| -bi | Executes the %prep, %build, and %install commands from the .spec file. |
| -bl | Checks for the existence of cited files. |
| -bp | Executes just the %prep stage of the spec file. |
| -bs | Builds just the source RPM package. |