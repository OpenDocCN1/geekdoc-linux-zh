
![](img/d75cffbcb54aabfb0f9854162061d394_72_0.png)

Figure 4.1: Base Filesystem Hierarchy Specified by the FHS

community in general have already established the `/opt/` directory for add-on software. The following list is a compilation of best practices for installing applications.

> In the following list, `package` is the product name of an application and `provider` is a LANANA-registered vendor name.

- The applications of the base operating system, or “the Linux distribution,” are the only ones allowed to be installed in the `/sbin/`, `/bin/`, and `/usr/` directories.
- System administrators who build packages from source—either source packages (`srpm`) or tape-archives (`tar`)—should install in the `/usr/local/bin/` directory, and must avoid the temptation to install in the `system` directories.
- Add-on binary-only packaged applications must be installed in the `/opt/package/` or `/opt/provider/` directory. For example, the binary executables should reside in their respective `/opt/provider/bin/` directories.
- Manual pages for applications must be located in their respective `/opt/package/share/man/` or `/opt/provider/share/man/` directories. Documentation other than man pages should be located in the corresponding `/opt/package/share/doc/` or `/opt/provider/share/doc/` directories.
- Host-specific configuration files for `/opt/` binary executables should go in the `/etc/opt/package/` or `/etc/opt/provider/` directory (all host-specific system configuration files reside in these directories).

Variable files in a package, or files that change during the normal course of system runtime, go in the `/var/opt/package/` and `/var/opt/provider/` directories.

Exceptions can be made to these rules if it is necessary for a package to install or create files elsewhere. For example, if a package creates a new device, it installs in the `/dev/` directory.

The system administrator should create a separate disk partition for the `/opt/` filesystem, and end users should add `/opt/package/bin/` and `/opt/bin/` to their PATH environment variables. Usually the end user's shell will find applications in their respective `/opt/package/bin/` directories; however, the system administrator may have created symbolic links or wrapper scripts in `/opt/` for each package using setup-opt.sh.

```bash
# setup-opt.sh /opt/whizbang/bin/widgets
# setup-opt.sh /opt/whizbang/man/man1/widgets.1
```

## 4.3 PACKAGE NAMING

To avoid conflicts between native distribution packages and LSB-conformant packages, a naming scheme was specified. Names of all LSB-compliant packages begin with `lsb-`. If the name of the package contains only one hyphen, then the name must be assigned by the Linux Assigned Names and Numbers Authority.[^6] If the name of the package contains more than one hyphen, then the portion of the package name between the first and second hyphens must be either an LSB provider name assigned by the LANANA, or one of the owner's fully-qualified domain names in lowercase.

### 4.3.1 Init Script Naming

The LANANA init script names are used by LSB-compliant applications and distributions when naming init scripts placed in the `/etc/init.d` directory. Alternatively, it is also possible to use a script name that begins with your fully qualified Internet domain name or your LSB provider name.

> 6. http://www.lanana.org/

Since all init scripts live in the same directory, a similar scheme has been specified to avoid clashes between init scripts for packages. The LSB Written Specification states that init scripts can be in one of three namespaces:

1. **Assigned namespace**: This namespace consists of names that only use the character set `[a-z0-9]`. These names must be reserved through LANANA.
2. **Hierarchical namespace**: This namespace consists of script names that look like this: `[hier1]-[hier2]-...-[name]`, where *name* uses the character set `[a-z0-9]` and there may be one or more [hier*n*] components. The [hier*1*] may either be an LSB provider name assigned by the LANANA, or it may be the owner’s DNS name in lower-case, with at least one period character (".").
3. **Reserved namespace**: This namespace consists of script names that begin with the underscore character ("_"), and it is reserved for distribution use only. This namespace should be used for core packages only, and in general, use of this namespace is highly discouraged.

### 4.3.2 Cron Script Naming

The LANANA Cron Script registry defines a reserved list of script names to be used in the `/etc/cron.d` directory in an LSB Runtime Environment. Alternatively, it is also possible to use a script name that begins with your fully qualified Internet domain name or your LSB provider name.

## 4.4 EXAMPLE: PACKAGING AND INSTALLING AN APPLICATION

Example 4.1 shows how to package and install a fictional software suite called Widgets according to LSB packaging specifications. The `widgets-1.2.3.spec` RPM configuration file is used to package the software for the `/opt/` directory. The `@files` directive (line 17) is followed by a list of pathnames which should be packaged. The `@prefix` tag (line 8) is how the package is made relocatable. The value of the tag defines the part of the path that can be varied at installation time.

### Example 4.1: RPM Spec File for Widgets

```text
#
# RPM Package Manager (RPM) spec file for Widgets :-)
#
Summary: Some generic program
Name: widgets
Version: 1.2
Release: 3
Prefix: /opt
Copyright: Commercial
Group: Application/Productivity
URL: http://www.whizbangwidgets.com/
Vendor: WhizBang Widgets
Packager: John Doe <jd@whizbangwidgets.com>
%description
This is a demonstration of a relocatable RPM package for a fictional productivity application.
%files
/opt/whizbang/bin/widgets
/opt/whizbang/man/widgets.1
/etc/opt/whizbang/widgets.conf
# Post-install stuff would go here.
%E0F
```

1. Build the RPM package for Widgets (widgets-1.2-3.i486), as shown in Example 4.2, using widgets-1.2-3.spec as the input file. You can use rpm to build and produce a source package file (widgets-1.2-3.src.rpm) and a binary package file (widgets-1.2-3.i486.rpm) from this input.

### Example 4.2: Building an RPM Package for Widgets

```bash
# rpm -ba /usr/src/redhat/SPECS/widgets-1.2-3.spec
Processing files: widgets
Finding provides...
Finding requires...
Prereqs: /bin/sh
Wrote: /usr/src/redhat/SRPMS/widgets-1.2-3.src.rpm
Wrote: /usr/src/redhat/RPMS/i486/widgets-1.2-3.i486.rpm
```

2. Install Widgets on the system from the binary package (`widgets-1.2-3.i486.rpm`), as shown in Example 4.3.

### Example 4.3: Installing an RPM Package for Widgets

```bash
# rpm -i /usr/src/redhat/RPMS/i486/widgets-1.2-3.i486.rpm
```

Widgets is now installed in `/opt/whizbang/bin/`.

3. Run Widgets from the command line, as shown in Example 4.4.

### Example 4.4: Running Widgets

```bash
$ /opt/whizbang/bin/widgets
```

4. As the system administrator, create a symbolic link to `/opt/whizbang/bin/widgets` from `/opt/bin/widgets`, and to `/opt/whizbang/lib/libwidget.so` from `/opt/lib/libwidget.so` (Example 4.5). Per the FHS, this cannot be done at the post-install stage automatically because the package does not own the `/opt/bin/` directory domain. Only the system administrator has the authority to make a global configuration that may impact other applications.

### Example 4.5: Manually Creating Symbolic Links for Widgets

```bash
# ln -s /opt/whizbang/bin/widgets /opt/bin/widgets
# ln -s /opt/whizbang/lib/libwidget.so /opt/lib/libwidget.so
```

As illustrated in Figure 4.2, the symbolic link will make it easier for the end user to run Widgets.

5. Uninstall the `widgets-1.2-3` RPM package, and reinstall it in an alternate location in the `/usr/local` directory, as shown in Example 4.6.

The system administrator should not forget to fix any manual symbolic links that may have been made in `/opt/bin/`.

![](img/d75cffbcb54aabfb0f9854162061d394_77_0.png)

Figure 4.2: Simple Packaging

### Example 4.6: Relocating Widgets

```bash
# rpm -e widgets-1.2-3
# cd /usr/src/redhat/RPMS/i486/
# rpm -i --prefix /usr/local widgets-1.2-3.i486.rpm
```

## 4.5 ADVANCED PACKAGING

It has been demonstrated that add-on binary-only applications are to be installed in the `/opt/package/bin/` and `/opt/provider/bin/` directories. The basics of creating a flexible relocatable RPM package have been demonstrated by being able to override the default `/opt/` destination and select an alternate location. Now let’s look at more advanced scenarios involving packaging multiple products, packaging for multiple architectures, packaging for multiple versions of a product, or any combinations thereof.

### 4.5.1 Packaging Multiple Products

Recall the WhizBang Widgets example in this chapter. What if you want to ship another product called Gadgets? To support multiple products by one vendor, they should all be based off of the `/opt/provider/package/` directory as illustrated in Figure 4.3. Since the LANANA-registered WhizBang owns
