And what happens if the build environment isn't ready and a `--short-circuit` is attempted? Let's see:

```
# rpm -bi --short-circuit ccdplayer-1.0.spec
\* Package: ccdplayer
+ umask 022
+ echo Executing: %install
Executing: %install
+ cd /usr/src/redhat/BUILD
+ cd ccdplayer-1.0
/var/tmp/rpmbu01157aaa: ccdplayer-1.0: No such file or directory
Bad exit status
#
```

RPM blindly started executing the `%install` stage, but came to an abrupt halt when it attempted to change directory into `ccdplayer-1.0`, which didn't exist. After giving a descriptive error message, RPM exited with a failure status. Except for some minor differences, `rpm -bc` would have failed in the same way.

# ## 12.1.8. `--buildarch <arch>`: Perform a Build for the `<arch>` Architecture

The `--buildarch` option is used to override RPM's architecture detection logic. The option is followed by the desired architecture name. Here's an example:

```
# rpm -ba --buildarch i486 ccdplayer-1.0.spec
Package: ccdplayer
...\nBinary Packaging: ccdplayer-1.0-1
...\nWrote: /usr/src/redhat/RPMS/i486/ccdplayer-1.0-1.i486.rpm
...\nWrote: /usr/src/redhat/SRPMS/ccdplayer-1.0-1.src.rpm
#
```

We've removed most of RPM's output from this example, but the main thing we can see from this example is that the package was built for the i486 architecture, due to the inclusion of the `--buildarch` option on the command line. We can also see that RPM wrote the binary package in the architecture-specific directory, `/usr/src/redhat/RPMS/i486`. Using RPM's `--queryformat` option confirms the package's architecture:

```
# rpm -qp --queryformat '%{arch}\n'\
> /usr/src/redhat/RPMS/i486/ccdplayer-1.0-1.i486.rpm
i486
#
```

For more information on build packages for multiple architectures, see Chapter 19, "Building Packages for Multiple Architectures and Operating Systems."