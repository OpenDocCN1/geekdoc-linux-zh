
Simple text files, with the same syntax described above and the `.list` file extension.

Below you see the contents of a file called `/etc/apt/sources.list.d/buster-backports.list`:

```
deb http://deb.debian.org/debian buster-backports main contrib non-free
deb-src http://deb.debian.org/debian buster-backports main contrib non-free
```

### Listing Package Contents and Finding Files

A utility called `apt-file` can be used to perform more operations in the package index, like listing the contents of a package or finding a package that contains a specific file. This utility may not be installed by default in your system. In this case, you can usually install it using `apt-get`:

```
# apt-get install apt-file
```

After installation, you will need to update the package cache used for `apt-file`:

```
# apt-file update
```

This usually takes only a few seconds. After that, you are ready to use `apt-file`.

To list the contents of a package, use the `list` parameter followed by the package name:

```
# apt-file list unrar
unrar: /usr/bin/unrar-nonfree
unrar: /usr/share/doc/unrar/changelog.Debian.gz
unrar: /usr/share/doc/unrar/copyright
unrar: /usr/share/man/man1/unrar-nonfree.1.gz
```

> **TIP** You can also use `apt list` instead of `apt-file list`.

You can search all packages for a file using the `search` parameter, followed by the file name. For example, if you wish to know which package provides a file called `libSDL2.so`, you can use:

```
# apt-file search libSDL2.so
libSDL2-dev: /usr/lib/x86_64-linux-gnu/libSDL2.so
```

The answer is the package `libSDL2-dev`, which provides the file `/usr/lib/x86_64-linux-gnu/libSDL2.so`.

The difference between `apt-file search` and `dpkg-query` is that `apt-file search` will also search uninstalled packages, while `dpkg-query` can only show files that belong to an installed package.

## Guided Exercises

- 1. What is the command to install a package named `package.deb` using `dpkg`?
- 2. Using `dpkg-query`, find which package contains a file named `7zr.1.gz`.
- 3. Can you remove a package called `unzip` from the system using `dpkg -r unzip` if the package `file-roller` depends on it? If not, what would be the correct way to do it?
- 4. Using `apt-file`, how can you find out which package contains the file `unrar`?
- 5. Using `apt-cache`, what is the command to show information for the package `gimp`?

## Explorational Exercises

- 1. Consider a repository with Debian source packages for the `xenial` distribution, hosted at `http://us.archive.ubuntu.com/ubuntu/` and with packages for the `universe` component. What would be the corresponding line to be added to `/etc/apt/sources.list`?
- 2. While compiling a program, you come across an error message complaining that the header file `zzip-io.h` is not present in your system. How can you find out which package provides that file?
- 3. How can you ignore a dependency warning and remove a package using `dpkg`, even if there are packages that depend on it in the system?
- 4. How can you get more information about a package called `midori` using `apt`?
- 5. Before installing or updating packages with `apt`, which command should be used to ensure that the package index is up-to-date?

## Summary

In this lesson, you learned:

- How to use **dpkg** to install and remove packages.
- How to list installed packages and package contents.
- How to reconfigure an installed package.
- What is **apt**, and how to install, upgrade and remove packages using it.
- How to use **apt-cache** to search for packages.
- How the `/etc/apt/sources.list` file works.
- How to use **apt-file** to show the contents of a package, or how to find which package contains a specific file.

The following commands were discussed:

**dpkg -i**

Installs a single package, or a space-separated list of packages.

**dpkg -r**

Removes a package, or a space-separated list of packages.

**dpkg -I**

Inspects a package, providing details on the software it installs and any needed dependencies.

**dpkg --get-selections**

Lists out every package that dpkg has installed on the system.

**dpkg -L**

Prints out a list of every file that a particular package installs.

**dpkg-query**

With a specified file name, this command will print out the package that installed the file.

**dpkg-reconfigure**

This command will re-run a packages _post-install_ script so that an administrator can make configuration adjustments to the package’s installation.

**apt-get update**

This command will update the local package index to match what is available within the configured repositories under the `/etc/apt/` directory.

**apt-get install**

This command will download a package from a remote repository and install it along with its dependencies, can also be used to install a Debian package that has already been downloaded.

**apt-get remove**

This command will uninstall the specified package(s) from the system.

**apt-cache show**

Just like the `dpkg -I` command, this command can be used to show details on a specific package.

**apt-cache search**

This command will search your local APT cached database for a particular package.

**apt-file update**

This command will update the package cache so that the `apt-file` command can query its contents.

**apt-file search**

This command will search in which package a file is included. A list of all packages containing the pattern is returned.

**apt-file list**

This command is used to list the contents of a package, just like the `dpkg -L` command.

## Answers to Guided Exercises

1. What is the command to install a package named `package.deb` using dpkg?

Pass the `-i` parameter to dpkg:

```
# dpkg -i package.deb
```

2. Using `dpkg-query`, find which package contains a file named `7zr.1.gz`.

Add the `-S` parameter to `dpkg-query`:

```
# dpkg-query -S 7zr.1.gz
```

3. Can you remove a package called `unzip` from the system using `dpkg -r unzip` if the package `file-roller` depends on it? If not, what would be the correct way to do it?

No. `dpkg` will not resolve dependencies, and will not let you remove a package if another installed package depends on it. In this example, you could first remove `file-roller` (assuming nothing depends on it) and then remove `unzip`, or remove both at the same time with:

```
# dpkg -r unzip file-roller
```

4. How can you find out which package contains the file `/usr/bin/unrar` using the `apt-file` utility?

Use the `search` parameter followed by the path (or filename):

```
# apt-file search /usr/bin/unrar
```

5. Using `apt-cache`, what is the command to show information for the package `gimp`?

Use the `show` parameter followed by the package name:

```
# apt-cache show gimp
```

## Answers to Explorational Exercises

1. Consider a repository with Debian source packages for the `xenial` distribution, hosted at `http://us.archive.ubuntu.com/ubuntu/` and with packages for the `universe` component. What would be the corresponding line to be added to `/etc/apt/sources.list`?

Source packages are of the `deb-src` type, so the line should be:

```
deb-src http://us.archive.ubuntu.com/ubuntu/ xenial universe
```

This line could also be added inside a `.list` file in `/etc/apt/sources.list.d/`. The name is up to you but should be descriptive, something like `xenial_sources.list`.

2. While compiling a program, you come across an error message complaining that the header file `zzip-io.h` is not present on your system. How can you find out which package provides that file?

Use `apt-file search` to find which package contains a file not present in the system:

```
# apt-file search zzip-io.h
```

3. How can you ignore a dependency warning and remove a package using `dpkg`, even if there are packages that depend on it in the system?

The parameter `--force` can be used, but this should *never* be done unless you know exactly what you are doing, since there is a great risk that your system will be left in an inconsistent or “broken” state.

4. How can you get more information about a package called `midori` using `apt-cache`?

Use `apt-cache show` followed by the package name:

```
# apt-cache show midori
```

5. Before installing or updating packages with `apt-get`, which command should be used to ensure that the package index is up-to-date?

`apt-get update` should be used. This will download the latest package indexes from the repositories described in the `/etc/apt/sources.list` file or in the `/etc/apt/sources.list.d/` directory.
