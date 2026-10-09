FreeBSD ships with a very simple package manager in /usr/sbin/pkg, pkg(7). It has barely enough brains to find FreeBSD’s current package manager. It installs that new package manager and surrenders all responsibility for package management to it. This gives FreeBSD the flexibility to update the package manager with the packages.

The first time you try to install a package, pkg(8) prompts you to install the package manager. I found I needed the dmidecode package on a new server, so I can get an RMA on a bad power supply from the manufacturer. (Don’t worry about how I *found* the dmidecode package—just go with me for the moment.)

```
# pkg install dmidecode
```

FreeBSD runs pkg(8) and finds that no package management is installed yet.

```
The package management tool is not yet installed on your system.
Do you want to fetch and install it now? [y/N]: y
```

The default answer appears in capital letters. If I hit **n** and **ENTER**, pkg terminates. If I hit **y** and **ENTER**, FreeBSD bootstraps the system.

```
① Bootstrapping pkg from pkg+http://pkg.FreeBSD.org/FreeBSD:12:amd64:quarterly,
  please wait...
② Verifying signature with trusted certificate pkg.freebsd.org.2013102301...
  done
③ Installing pkg-1.10.0_2...
  Extracting pkg-1.10.0_2: 100%
④ Updating FreeBSD repository catalogue...
  meta.txz                              : 100%   944 B   0.9kB/s   00:01
  packagesite.txz                       : 100%   6 MiB   2.0MB/s   00:03
  Processing entries: 100%
FreeBSD repository update completed. 26059 packages processed.
All repositories are up to date.
Updating database digests format: 100%
```

The installation starts by downloading the current pkg tools from a FreeBSD mirror ① . It then checks the digital signature on the downloaded file ② . The tools are extracted and installed ③ . Pkg then downloads and installs the catalog of available packages ④ .