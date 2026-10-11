# 12.1.9. --builddos <os>: Perform Build for the <os> Operating System

The `--builddos` option is used to override RPM's operating system detection logic. The option is followed by the desired operating system name. Here's an example:

```
# rpm -ba --builddos osf1 cdpLayer-1.0.spec
...
Binary Packaging: cdpLayer-1.0-1
...
Wrote: /usr/src/redhat/RPMS/i386/cdpLayer-1.0-1.i386.rpm
Source Packaging: cdpLayer-1.0-1
...
Wrote: /usr/src/redhat/SRPMS/cdpLayer-1.0-1.src.rpm
#
```

There is nothing in the build output that explicitly states that the build operating system has been set to osf1. Let's see if `--queryformat` will tell us:

```
# rpm -qp --queryformat '%{os}\n' \
> /usr/src/redhat/RPMS/i386/cdpLayer-1.0-1.i386.rpm
osf1
#
```

The package was indeed built for the specified operating system. For more information on building packages for multiple operating systems, see Chapter 19.

# 12.1.10. --sign: Add a Digital Signature to the Package

The `--sign` option directs RPM to add a digital signature to the package being built. Currently, this is done using PGP. Here's an example of `--sign` in action:

```
# rpm -ba --sign cdpLayer-1.0.spec
Enter pass phrase: <passphrase> (not echoed)
Pass phrase is good.
Package: cdpLayer
...
Binary Packaging: cdpLayer-1.0-1
...
Generating signature: 1002
Wrote: /usr/src/redhat/RPMS/i386/cdpLayer-1.0-1.i386.rpm
...
Source Packaging: cdpLayer-1.0-1
...
Generating signature: 1002
Wrote: /usr/src/redhat/SRPMS/cdpLayer-1.0-1.src.rpm
#
```

The most obvious effect of adding the `--sign` option to a build command is that RPM then asks for your private key's passphrase. After entering the passphrase (which isn't echoed), the build proceeds as usual. The only other difference between this and a nonsigned build is that the Generating signature: lines have a nonzero value.