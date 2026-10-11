That didn’t go very well. Let’s see what adding `--replacepkgs` will do:

```
# rpm -iv --replacepkgs cdp-0.33-2.1386.rpm
# Installing cdp-0.33-2.1386.rpm
#
```

Much better. The original package was replaced by a new copy of itself.

# 2.4.4. --replacefiles: Install the Package Even if It Replaces Another Package’s Files

While the `--replacepkgs` option permits a package to be installed on top of itself, `--replacefiles` is used to allow a package to overwrite files belonging to a different package. Sounds strange? Let’s go over it in a bit more detail.

One thing that sets RPM apart from many other package managers is that it keeps track of all the files it installs in a database. Each file’s database entry contains a variety of information about the file, including a means of summarizing the file’s contents. By using these summaries, known as MD5 checksums, RPM can determine whether a particular file is going to be replaced by a file with the same name but different contents. The following paragraphs give an example.

> **NOTE**
> We’ll get more into this aspect of RPM in Chapter 6, “Using RPM to Verify Installed Packages,” when we discuss `rpm -V`.

Package A installs a file (we’ll call it `/bin/foo.bar`). When Package A is installed, `foo.bar` resides happily in the `/bin` directory. In the RPM database, there is an entry for `/bin/foo.bar`, including the file’s MD5 checksum.

However, there is another package, B. Package B also has a file called `foo.bar` that it wants to install in `/bin`. There can’t be two files in the same directory with the same name. The files are different; their MD5 checksums do not match. What happens if Package B is installed? Let’s find out. Here, we’ve installed a package:

```
# rpm -iv cdp-0.33-2.1386.rpm
# Installing cdp-0.33-2.1386.rpm
#
```

Okay, no problem there. But we have another package to install. In this case, it is a new release of the `cdp` package. Note that RPM’s detection of file conflicts does not depend on the two packages being related. It is strictly based on the name of the file, the directory in which it resides, and the file’s MD5 checksum. Here’s what happens when we try to install the package:

```
# rpm -iv cdp-0.33-3.1386.rpm
# Installing cdp-0.33-3.1386.rpm
```