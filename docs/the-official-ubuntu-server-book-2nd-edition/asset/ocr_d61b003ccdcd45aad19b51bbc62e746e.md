root). Of course, the package may also require build dependencies that are not installed by running a command in the following form:

```
# apt-get -t jaunty build-dep most
```

The build-dep subcommand to apt-get automates the process of installing all software necessary to build a given package. Running it is a frequent first step in rebuilding any package for the first time when that package is from an installed repository.

When the software in question is successfully rebuilt, the directory will contain a set of binary packages for this source package that end with .deb in the directory where it is run. In this case, the single binary package created was called most 5.0.0a-1 i386.deb. The -1 following the version number of the software refers to the version of the package and could be incremented each time we made a new version of the package. The i386 in this case simply refers to the architecture for which the binary package was built. In this case, I built it on an Intel machine. For many users, this will say amd64, which is an increasingly popular architecture. For most interpreted programs that will run on any architectures, this will say all.

# New Upstream Versions

New upstream versions of packages are slightly more complicated than simply rebuilding an existing package with no modifications. Installing the package devscripts provides the user with a program called usupdate which helps with this process. To use usupdate, a user must first download the source package with a command like apt-get source most. Leave off the compile option for the moment, and then download the new upstream version tarball. There is no reason to unpack it at this point and, optionally, rename it into name-version.tar.gz format. Changing into the directory of the old package's source and running usupdate with the new upstream tarball as the argument will usually do the trick:

```
$ cd most-5.0.0a $ usupdate ../most-5.0.1.tar.gz
```

Usually, usupdate then deduces the version number from the upstream tarball and applies all the changes made to the old version to the new upstream