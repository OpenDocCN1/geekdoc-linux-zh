# ### 2.4.8. --includedocs: Install Documentation for This Package

As the name implies, `--includedocs` directs RPM to install any files marked as being documentation. This option is normally not required, unless the `rpmrc` file entry `excludedocs: 1` is included in the referenced `rpmrc` file. Here's an example. Note that in this example, `/etc/rpmrc` contains `excludedocs: 1`, which directs RPM not to install documentation files:

```
```text
# ls /usr/man/man1/cdp.1
ls: /usr/man/man1/cdp.1: No such file or directory
# rpm -iv cdp-0.33-3.i386.rpm
Installing cdp-0.33-3.i386.rpm
# ls /usr/man/man1/cdp.1
ls: /usr/man/man1/cdp.1: No such file or directory
#```
```

Here we've checked to make sure that the `cdp` man page did not previously exist on the system. Then after installing the `cdp` package, we find that the `excludedocs: 1` in `/etc/rpmrc` did its job: The man page wasn't installed. Let's try it again, this time adding the `--includedocs` option:

```
```text
# ls /usr/man/man1/cdp.1
ls: /usr/man/man1/cdp.1: No such file or directory
# rpm -iv --includedocs cdp-0.33-3.i386.rpm
Installing cdp-0.33-3.i386.rpm
# ls /usr/man/man1/cdp.1
-rw-r--r-- 1 root root 4550 Apr 24 22:37 /usr/man/man1/cdp.1
#```
```

The `--includedocs` option overrode the `rpmrc` file's `excludedocs: 1` entry, causing RPM to install the documentation file.

# ### 2.4.9. -prefix <path>: Relocate the Package to <path>, if Possible

Some packages give the person installing them flexibility in determining where on his system they should be installed. These are known as *relocatable packages*. A relocatable package differs from a package that cannot be relocated in only one way—the definition of a default prefix. Because of this, it takes a bit of additional effort to determine whether a package is relocatable. But here's an RPM command that can be used to find out:

```
```bash
rpm -qp --qrfmt "%{defaultprefix}\n" <packagefile>```
```

> **NOTE**
> 
> You can find more about RPM's query commands in Chapter 5, "Getting Information About Packages."