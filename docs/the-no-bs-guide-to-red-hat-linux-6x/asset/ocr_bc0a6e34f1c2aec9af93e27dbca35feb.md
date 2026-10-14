# To learn about a package before installing it, enter

```
rpm -qip hotrod-1.0-1.i386.rpm
Name         : hotrod          Distribution: Red Hat Linux
Version      : 1.0             Vendor: Faster Software
Release      : 1              Build Date: Sun Jul 04 14:35:27 1999
Install date : (none)          Build Host: dev.faster.com
Group        : Games           Source RPM: hotrod-1.0-1.src.rpm
Size         : 3143593
Summary      : simulated hotrod racing game for SVGA
Description  :
An action game that pits you against other maniacal drivers
on the Los Angeles freeway. Experience the thrill of road
rage as you attempt to get to work on time.
```

# To see what files a package contains, enter

```
rpm -qlp hotrod-1.0-1.i386.rpm
/usr/man/man1/hotrod.1
/usr/info/hotrod.info.gz
/usr/doc/hotrod-1.0-1/README
/usr/lib/games/hotrodlib/cars.dat
/usr/lib/games/hotrodlib/drivers.dat
/usr/lib/games/hotrodlib/weapons.dat
/usr/lib/games/hotrodlib
/usr/games/hotrod
```

# To find all installed packages that match a specific pattern, enter

```
rpm -qa | grep panda
panda-2.0-1
pandacalc-3.1-4
xpanda-1.2-3
```

Since the -q flag does accept a package name, you might wonder why we didn't use a command like this:

```
rpm -q panda*
```

This won't work because of the way the Bash shell treats wildcard characters, so we have to tell RPM to spit out all the installed package names and use grep to filter the list.
Finally, here's an advanced form of the query command that will tell you which packages are taking up the most room:

```
rpm -qa --queryformat="%(SIZE) %(NAME)" | sort -n
```