Build the binary RPM with

```
# rpmbuild -bb freetype.spec
```

During the build process, RPM will detect a patch and ask you about the patch; type y for “yes” to continue.

The new RPMs (actually four of them) are found in /usr/src/redhat/RPMS/i386. We need only the one named freetype_2.1.9, you can install it with rpm -Uvh. (This is why we changed the version number. if we had not, RPM would not upgrade to the “same” version. Had we not changed the version number, we could have forced the installation with the --replacepackages --replacefiles option.)

The font server needs to be restarted to use the new library, so we use the service command as shown in Chapter 15, “Automating tasks.”

```
# service xfs restart
```

Enjoy your new look—provided by better rendering of the fonts.

# Compile from Source Tarballs

Compiling applications from source is not that difficult. Most source code is available as compressed source tarballs—that is, tar files that have been compressed using gzip or bzip. The compressed files typically uncompress into a directory containing several files. It is always a good idea to compile source code as a regular user to limit any damage that broken or malicious code might inflict, so create a directory named source in your home directory.

From wherever you downloaded the source tarball, uncompress it into the ~/source directory using the -C option to tar:

```
$ tar zxvf packagename.tgz -C ~/source
```

```
$ tar zxvf packagename.tar.gz -C ~/source
```

```
$ tar jxvf packagename.bz -C ~/source
```

```
$ tar jxvf packagename.tar.bz2 -C ~/source
```

If you are not certain what file compression method was used, employ the file command to figure it out:

```
$ file packagename
```

Now, change directories to ~/source/packagename and look for a file named README, INSTALL, or a similar name. Print out the file if necessary because it contains specific