The basic syntax of alien is as follows:

```
alien [options] file[...]
```

The most important options are `--to-deb`, `--to-rpm`, `--to-slp`, and `--to-tgz`, which convert to Debian, RPM, Stampede, and tarball format, respectively. (If you omit the destination format, alien assumes you want a Debian package.) The `--install` option installs the converted package and removes the converted file. Consult the alien man page for additional options.

For instance, suppose you have a Debian package called someprogram-1.2.3-4.i386.deb, and you want to create an RPM from it. You can issue the following command to create an RPM called someprogram-1.2.3-5.i386.rpm:

```
# alien --to-rpm someprogram-1.2.3-4_i386.deb
```

If you use a Debian-based system and want to install a tarball but keep a record of the files it contains in your Debian package database, you can do so with the following command:

```
# alien --install binary-tarball.tar.gz
```

It’s important to remember that converting a tarball converts the files in the directory structure of the original tarball using the system’s root directory as the base. Therefore, you may need to unpack the tarball, juggle files around, and repack it to get the desired results prior to installing the tarball with alien. For instance, suppose you’ve got a binary tarball that creates a directory called program-files, with bin, man, and lib directories under this. The intent may have been to unpack the tarball in /usr or /usr/local and create links for critical files. To convert this tarball to an RPM, you can issue the following commands:

```
# tar xvfz program.tar.gz
# mv program-files usr
# tar cvfz program.tgz usr
# rm -r usr
# alien --to-rpm program.tgz
```

By renaming the program-files directory to usr and creating a new tarball, you’ve created a tarball that, when converted to RPM format, will have files in the locations you want—/usr/bin, /usr/man, and /usr/lib. You might need to perform more extensive modifications, depending on the contents of the original tarball.

# Package Dependencies and Conflicts

Although package installation often proceeds smoothly, sometimes it doesn’t. The usual sources of problems relate to unsatisfied dependencies or conflicts between packages. The RPM and Debian package management systems are intended to help you locate and resolve such problems, but on occasion (particularly when mixing packages from different vendors), they can actually cause problems. In either event, it pays to recognize these errors and know how to resolve them.