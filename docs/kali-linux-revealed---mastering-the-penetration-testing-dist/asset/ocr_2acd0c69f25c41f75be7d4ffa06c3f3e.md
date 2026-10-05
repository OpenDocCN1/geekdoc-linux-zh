not this command because it removes it automatically as soon as they are identified. In all cases, the tools display a clear message listing the affected packages.

It is a good habit to mark as automatic any package that you don't need directly so that they are automatically removed when they aren't necessary anymore. You can use apt-mark package to mark the given package as automatic, whereas apt-mark package does the opposite. aptitude mark and aptitude unmark in the same way, although they offer more features for marking many packages at once (see section 8.2.7.1, Aptitude [page 190]). The console-based interactive interface of aptitude also makes it easy to remove the automatic flag on many packages.

You might want to know why an automatically installed package is present on the system. This information from the command line, you can use aptitude why package (apt and apt-get) have no similar feature:

+   $ aptitude why python-debian
| aptitude Recommends apt-xapian-index
| A apt-xapian-index Depends python-debian (>= 0.1.15)

# 8.3.5. Leveraging Multi-Arch

All Debian packages have an Architecture field in their control information. This field can contain either "all\(for packages that are architecture-independent) or the name of the architecture that it targets (like amd64, or armhf). In the latter case, by default, dpkg will only install the package if its architecture matches the host's architecture returned by dpkg --print-architecture. This restriction ensures that you not end up with binaries compiled for an incorrect architecture. Everything would be perfect except that (some) computers can run binaries for multiple architectures, either natively (an amd64 system can run i386 binaries) or through emulators.

# Enabling Multi-Arch

Multi-arch support for dpkg allows users to define foreign architectures that can be installed on the current system. This is easily done with dpkg --add-architecture, as in the example below where the i386 architecture needs to be added to the amd64 system in order to run applications using Wine⁵ There is a corresponding dpkg --remove-architecture to drop support of a foreign architecture, but it can only be used when no packages of this architecture remain installed.

```
$ dpkg --print-architecture
amd64
```

> https://www.winehq.org/