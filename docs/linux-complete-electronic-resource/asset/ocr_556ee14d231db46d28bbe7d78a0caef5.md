+   *   `--noscripts`	Don't execute the preinstall or postinstall scripts.
+   *   `--notriggers`	Don't execute scripts which are triggered by the installation of this package.
+   *   `--excludedocs`	Don't install any files which are marked as documentation (which includes man pages and texinfo documents).
+   *   `--includedocs`	Install documentation files. This is only needed if *excludedocs: 1* is specified in an rpmc file.
+   *   `--test`	Do not install the package, simply check for and report potential conflicts.
+   *   `--prefix <path>`	This sets the installation prefix to `<path>` for relocatable packages.
+   *   `--ignoresarch`	This allows installation or upgrading even if the architectures of the binary RPM and host don't match.
+   *   `--ignoreos`	This allows installation or upgrading even if the operating systems of the binary RPM and host don't match.

# QUERY OPTIONS

The general form of an rpm query command is

```
rpm -q [query-options]
```

You may specify the format that package information should be printed in. To do this, you use the `--queryformat` option, followed by the format string.

Query formats are modified versions of the standard **printf(3)** formatting. The format is made up of static strings (which may include standard C character escapes for newlines, tabs, and other special characters) and **printf(3)** type formatters. As rpm already knows the type to print, the type specifier must be omitted however, and replaced by the name of the header tag to be printed, enclosed by `{}` characters. The **RPM\*** portion of the tag name may be omitted.

Alternate output formats may be requested by following the tag with **:type tag**. Currently, the following types are supported: *octal*, *date*, *sheepse*, *perms*, *flags*, and *deps.*

For example, to print only the names of the packages queried, you could use %{NAME} as the format string. To print the package's name and