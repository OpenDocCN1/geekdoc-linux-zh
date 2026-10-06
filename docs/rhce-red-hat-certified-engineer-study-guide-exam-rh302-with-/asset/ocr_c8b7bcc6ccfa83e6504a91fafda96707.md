# TABLE 12.2 Source Flags of the rpm Command (continued)

| Flag | Meaning |
| --- | --- |
| -bc | %build stage: make install |
| -bb | builds binary package |
| -ba | builds binary and source packages |
| --test | check syntax of SPEC file |

If a SPEC file is contained within a TAR file, you need to unpack the TAR file. Instead, replace the -b flag with -t and specify the TAR file that contains the SPEC file. The rpm command supports both uncompressed and gzip-compressed TAR files.

You need not install a source RPM in order to compile. Simply specify a command of the

```
rpm --recompile source_package_file
```

source_package_file is the name of the source RPM. To compile an uninstalled SRPM, build a corresponding binary RPM, and clean up the source files, issue a command of the

```
rpm --rebuild source_package_file
```

source_package_file is the name of the source RPM.

> The current RHCE guidelines require only conceptual understanding of source RPMs and related RPM commands. You don't need to be an expert in working with source RPMs.

![](bbox=[0.186, 0.663, 0.258, 0.715])

# GnoRPM

Any desktop Linux users prefer a graphical user interface to a command line interface. GnoRPM provides such users with an easy-to-use tool for manipulating RPM packages. Figure 12.2 shows the GnoRPM tool.