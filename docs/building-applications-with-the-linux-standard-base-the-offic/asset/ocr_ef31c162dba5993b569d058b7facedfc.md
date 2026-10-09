Since all init scripts live in the same directory, a similar scheme has been specified to avoid clashes between init scripts for packages. The LSB Written Specification states that init scripts can be in one of three namespaces:

+   1. **Assigned namespace**  This namespace consists of names that only use the character set `[a-z0-9]`. These names must be reserved through LANANA.

+   2. **Hierarchical namespace**  This namespace consists of script names that look like this: `[hier1]-[hier2]-...-[name]`, where *name* uses the character set `[a-z0-9]` and there may be one or more [hier*n*] components. The [hier*1*] may either be an LSB provider name assigned by the LANANA, or it may be the owner’s DNS name in lower-case, with at least one period character (".").

+   3. **Reserved namespace**  This namespace consists of script names that begin with the underscore character ("_"), and it is reserved for distribution use only. This namespace should be used for core packages only, and in general, use of this namespace is highly discouraged.

# 4.3.2 Cron Script Naming

The LANANA Cron Script registry defines a reserved list of script names to be used in the `/etc/cron.d` directory in an LSB Runtime Environment. Alternatively, it is also possible to use a script name that begins with your fully qualified Internet domain name or your LSB provider name.

# 4.4 EXAMPLE: PACKAGING AND INSTALLING AN APPLICATION

Example 4.1 shows how to package and install a fictional software suite called Widgets according to LSB packaging specifications. The `widgets-1.2.3.spec` RPM configuration file is used to package the software for the `/opt/` directory. The `@files` directive (line 17) is followed by a list of pathnames which should be packaged. The `@prefix` tag (line 8) is how the package is made relocatable. The value of the tag defines the part of the path that can be varied at installation time.