Since all of the start-up scripts invoked by init are symbolic links to those scripts in `/etc/rc/init.d`, when we need to make changes we need to modify only those in `/etc/rc.d/init.d`. Whenever you wish to add a start-up script, put the script in `/etc/rc.d/init.d` and then create appropriate `s*` and `k*` symbolic links in the various `/etc/rc/rc.d/rc*` (replace N with the appropriate number) directories. To disable functionality, say sendmail, you may remove or rename the symbolic links pointing to the sendmail start-up script, `/etc/rc.d/init.d/sendmail`.

The one exception to this structure is `/etc/rc.d/rc.local`. This file is symbolically linked to by `s991local` in `/etc/rc/rc.d/rc2.d`, `/etc/rc/rc3.d`, and `/etc/rc/rc5.d` by default. It is the last script invoked when the system enters run level 2, 3, or 5.

If this is your first look at run levels, it would be well worth your time to read the reference material noted in this section.

# RED HAT PACKAGE MANAGER

The Red Hat Package Manager (RPM) is the software that manages the *packages* on your Linux system. A package is a collection of related files that ordinarily provides a functional component of software (we say ordinarily because sometimes a package depends on other packages). RPM allows you to add, remove, build, query, and verify packages. Documentation for RPM is quite extensive, and the primary resources are listed in *RPM Resources* on page 28.

In this section, we will discuss a few RPM commands that we will revisit at various points in this book.

# Verifying Packages with RPM

RPM allows you to verify your installed packages and files. It can check each file's size (S), permissions or mode (M), the MD5 hash (5---see Hash Functions and Digital Signatures on page 44 for more information about MD5), major and minor numbers (D), symbolic link contents (L), owner (U), group (G), and modification time (T). It will also tell you if the file is a configuration file (c). It performs these checks against the originally installed configuration contained in the RPM database (a collection of files in `/var/lib/rpm`). Files and packages may be verified using the `-v` option. For example, we can verify `/etc/exports` and all of the files in the package that contain `/etc/exports` with

```
$ rpm -Vf /etc/exports
S.5....Tc /etc/exports
S.5....Tc /etc/hosts.allow
S.5....Tc /etc/hosts.deny
S.5....Tc /etc/printcap
S.5....Tc /etc/services
S.5....Tc /etc/exports
$
```