
- Control which aspects of a file are to be checked during package verification
- Eliminate some of the tedium in creating the %files list

In the %files list, one or more directives may be placed on a line, separated by spaces, before one or more filenames. Therefore, if %foo and %bar are two %files list directives, they may be applied to a file baz in the following manner:

```
%foo %bar baz
```

Now it's time to take a look at the directives that inhabit the %files list.

## 13.6.1. File-Related Directives

RPM processes files differently according to their types. However, RPM does not have a method of automatically determining file types. Therefore, it is up to the package builder to appropriately mark files in the %files list. This is done using one of the following directives.

Keep in mind that not every file will need to be marked. As you read the following sections, you'll see that directives are used only in special circumstances. In most packages, the majority of files in the %files list will not need to be marked.

### 13.6.1.1. The %doc Directive

The %doc directive flags the filename(s) that follow as being documentation. RPM keeps track of documentation files in its database so that a user can easily find information about an installed package. In addition, RPM can create a package-specific documentation directory during installation and copy documentation into it. Whether or not this additional step is taken depends on how a file is specified. Here is an example:

```
%doc  README
%doc /usr/local/foonly/README
```

The file README exists in the software's top-level directory during the build and is included in the package file. When the package is installed, RPM creates a directory in the documentation directory named the same as the package (that is, <software>-<version>-<release>) and copies the README file there. The newly created directory and the README file are marked in the RPM database as being documentation. The default documentation directory is /usr/doc and can be changed by setting the defaultdocdir rpmrc file entry. For more information on rpmrc files, see Appendix B.

The file /usr/local/foonly/README was installed into that directory during the build and is included in the package file. When the package is installed, the README file is copied into /usr/local/foonly and marked in the RPM database as being documentation.

The %config directive is used to flag the specified file as being a configuration file. RPM performs additional processing for config files when packages are erased, and during installations and upgrades. This is due to the nature of config files: They are often changed by the system administrator, and those changes should not be lost.

There is a restriction to the %config directive: No more than one filename may follow the %config. This means that the following example is the only allowable way to specify config files:

```
%config /usr/local/foonly/README
```
Note that the full path to the file, as it is installed at build time, is required.

The %attr directive permits finer control over three key file attributes:

- The file's permissions, or mode
- The file's user ID
- The file's group ID

The %attr directive has the following format:

```
%attr(<mode>, <user>, <group>) file
```

The mode is specified in the traditional numeric format, while the user and group are specified as a string, such as root. Here's a sample %attr directive:

```
%attr(755, root, root) foo.bar
```

This would set foo.bar's permissions to 755. The file would be owned by user root, group root. If a particular attribute does not need to be specified (usually because the file is installed with that attribute set properly), that attribute may be replaced with a dash:

```
%attr(755, -, root) foo.bar
```

The main reason to use the %attr directive is to permit users without root access to build packages. The techniques for doing this (and a more in-depth discussion of the %attr directive) can be found in Chapter 16.

RPM's ability to verify the integrity of the software it has installed is impressive. But sometimes it's a bit too impressive. After all, RPM can verify as many as nine different aspects of every file. The %verify directive can control which of these file attributes are to be checked when an RPM verification is done. Here are the attributes, along with the names used by the %verify directive:

- Owner (`owner`)
- Group (`group`)
- Mode (`mode`)
- MD5 Checksum (`md5`)
- Size (`size`)
- Major Number (`maj`)
- Minor Number (`min`)
- Symbolic Link String (`symlink`)
- Modification Time (`mtime`)

How is %verify used? Say, for instance, that a package installs device files. Since the owner of a device will change, it doesn't make sense to have RPM verify the device file's owner/group and give out a false alarm. Instead, the following %verify directive could be used:

```
%verify(mode md5 size maj min symlink mtime) /dev/tty$0
```

We've left out owner and group since we'd rather RPM not verify those. (RPM will automatically exclude file attributes from verification if it doesn't make sense for the type of file. In our example, getting the MD5 checksum of a device file is an example of such a situation.) However, if all you want to do is prevent RPM from verifying one or two attributes, you can use %verify's alternate syntax:

```
%verify(not owner group) /dev/tty$0
```

This use of %verify produces results identical to those in the previous example.

## 13.6.2. Directory-Related Directives

While the two directives in this section perform different functions, each is related to directories in some way. Let's see what they do.

### 13.6.2.1. The %docdir Directive

The %docdir directive is used to add a directory to the list of directories that will contain documentation. RPM includes the directories /usr/doc, /usr/info, and /usr/man in the %docdir list by default.

For example, if the following line is part of the %files list:

```
%docdir /usr/blather
```

any files in the %files list that RPM packages from /usr/blather will be included in the package as usual, but will also be automatically flagged as documentation. This directive is handy when a package creates its own documentation directory and contains a large number of files. Let's give it a try by adding the following line to our spec file:

```
%docdir /usr/blather
```

Our %files list contains no references to the several files the package installs in the /usr/blather directory. After building the package, looking at the package's file list shows this:

```
# rpm -qlp ../RPMS/i386/blather-1.0-1.i386.rpm
...
```

Wait a minute: There's nothing there, not even /usr/blather! What happened?

The problem is that %docdir only directs RPM to mark the specified directory as holding documentation. It doesn't direct RPM to package any files in the directory. To do that, we need to clue RPM in to the fact that there are files in the directory that must be packaged.

One way to do this is to simply add the files to the %files list:

```
%docdir /usr/blather
/usr/blather/INSTALL
```

Looking at the package, we see that INSTALL was packaged:

```
# rpm -qlp ../RPMS/i386/blather-1.0-1.i386.rpm
...
/usr/blather/INSTALL
```

Directing RPM to only show the documentation files, we see that INSTALL has indeed been marked as documentation, even though the %doc directive had not been used:

```
# rpm -qdqp ../RPMS/i386/blather-1.0-1.i386.rpm
...
/usr/blather/INSTALL
```

Of course, if you go to the trouble of adding each file to the %files list, it wouldn't be that much more work to add %doc to each one. So the way to get the most benefit from %docdir is to add another line to the %files list:

```
%docdir /usr/blather
/usr/blather
```

Since the first line directs RPM to flag any file in /usr/blather as being documentation, and the second line tells RPM to automatically package any files found in /usr/blather, every single file in there will be packaged and marked as documentation:

```
# rpm -qdq ../RPMS/i386/blather-1.0-1.i386.rpm
/usr/blather
/usr/blather/COPYING
```
