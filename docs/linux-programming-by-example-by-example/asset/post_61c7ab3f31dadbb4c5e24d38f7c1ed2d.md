
## Invoking tar

In its simplest form, the command to create a tarball is

```
$ tar cf archivename filelist
```

`c` says to create a tarball from the files indicated by `filelist`. `f` says to name the tarball `archivename`. You will generally want to compress the tarball to conserve disk space and minimize download time. The easiest way to do so, using GNU's `tar`, is to add `z` to the option list, which causes `tar` to invoke another GNU utility, `gzip`, on the tarball to compress it. In this case, the invocation would look like the following:

```
$ tar czf archivename filelist
```

![](img/be588b36b489136ce784030a08a1d3d4_489_0.png)

## Examples

- 1. The following `tar` invocation creates a tarball named `mytar.tar` from all the files in the `/etc` directory that end in `.conf`:

![](img/be588b36b489136ce784030a08a1d3d4_489_1.png)

### Output

```
$ tar cf mytar.tar /etc/*.conf
tar: Cannot add file /etc/amd.conf: Permission denied
tar: Removing leading '/' from absolute path names in the archive
tar: Cannot add file /etc/quota.conf: Permission denied
tar: Error exit delayed from previous errors
```

You might get errors because mortal users do not have access to certain files. In this case, `tar` will not add that file to the archive, but otherwise the archive will still be created.

![](img/be588b36b489136ce784030a08a1d3d4_489_2.png)

### Example

- 2. To list the contents of the archive, use the following command:

![](img/be588b36b489136ce784030a08a1d3d4_489_3.png)

### Output

```
$ tar tf mytar.tar
etc/dosemu.conf
etc/gpm-root.conf
etc/host.conf
etc/inetd.conf
etc/issapnp.conf
etc/ld.so.conf
etc/lilo.conf
etc/logrotate.conf
etc/named.conf
etc/nscd.conf
etc/nsswitch.conf
etc/ntp.conf
etc/pwdb.conf
etc/resolv.conf
etc/smb.conf
etc/syslog.conf
```

Note that `tar` does not remove any of the original files, but merely creates a new tarball.

![](img/be588b36b489136ce784030a08a1d3d4_491_0.png)

### Example

- 3. To create a compressed archive, simply add `z` to the option list. Traditionally, compressed tarballs, usually called *gripped tarballs*, are named by adding `.gz` to the end. They are also often given the extension `.tgz`. Either one is acceptable. For purposes of consistency, this chapter will add `.gz` to the end of the filename.

![](img/be588b36b489136ce784030a08a1d3d4_491_1.png)

### Output

```
$ tar czvf mytar.tar.gz /etc/*.conf
etc/dosemu.conf
etc/gpm-root.conf
etc/host.conf
etc/inetd.conf
etc/isapnp.conf
etc/ld.so.conf
etc/lilo.conf
etc/logrotate.conf
tar: Cannot add file /etc/quota.conf: Permission denied
tar: Error exit delayed from previous errors
etc/smb.conf
etc/syslog.conf
```

The `v` option instructs `tar` to be verbose, that is, to list the files it is adding to the archive. Again, it is safe to ignore errors that occur due to file access violations.

> **TIP**
> Using the `z` option to compress a tarball slows down `tar`'s operation somewhat, but it saves typing because you do not have to issue a second shell command, using `gzip`, to compress the tarball. On the other hand, calling `gzip` directly results in much better compression, but you have to type an additional command to prepare your package for distribution. Because programmers are lazy critters, makefiles usually include a target named `dist` that creates a gzipped tarball. This reduces the amount of typing you'll have to do and is convenient: simply type `make dist` and your package is ready to upload for the rest of the world to download.

Make sure you understand the difference between `gzip`, `zip`, and `compress`. `gzip` is the standard file compression utility on Linux systems. It is also the default compression utility used when you use `tar`'s `z` option. Compressed archives created using `gzip` generally have a `.gz` extension on them. `zip` creates PKZIP compatible files but is a free alternative to the PKZIP utilities. Files compressed using `zip` have a `.zip` extension. `compress`, finally, is one of the original UNIX utilities for compressing files. A file compressed using `compress` generally has a .Z extension.

## Updating tar Files

So, now you have a nicely packaged and compressed tarball. But, suddenly, you realize you neglected to include the documentation. You did write documentation, didn’t you? Never fear, you can easily add new files to (or update existing files in) the tarball using tar’s `append` or `update` options.

To append your newly written documentation to the compressed tarball we created at the end of the last series of examples, you can use the `r` option or the `u` option. The r instructs tar to append the specified files to the end of the tarball. u, on the other hand, simply updates a file presently in the archive with a newer version. Naturally, if it does not exist in the archive, it will be added.

![](img/be588b36b489136ce784030a08a1d3d4_492_0.png)

### Example

This command uses `u` to update files with newer copies.

```
$ tar uvf mytar.tar /etc/*.conf
```

The output is identical to that generated when you created the tarball, so it is not repeated here. Note that the command did not use the compression option, z. This is because GNU tar, at least as of version 1.12, cannot update compressed files. As a result, it was necessary to uncompress the tarball first, using `gunzip mytar.tar`.

## Deleting Files from Tarballs

To delete a file from a tarball, you have to use the long option `--delete` and specify the name of the files you want to delete. As with the update option, you cannot delete files from a compressed tarball.

![](img/be588b36b489136ce784030a08a1d3d4_492_1.png)

### Example

This example deletes `isapp.conf` and `host.conf` from the tarball created in earlier examples.

```
$ tar --delete -f=mytar.tar isapp.conf host.conf
```

Note that the file deletion operation does not have a convenient single letter option; you *must* use `--delete`.

## Using the install Command

Consider `install` a `cp` command on steroids. In addition to copying files, it sets their permissions and, if possible, their owner and group. It can also create destination directories if they do not already exist.

### Invoking install

install is normally used in makefiles as part of a rule for a target named (something like) install. It can also be used in shell scripts. The install command's general syntax is

```
$ install [option[...]] source[... ] dest
```

where source is one or more files to copy and dest is either the name of the target file or, if multiple files are specified in source, a directory. option can be one or more values listed in Table 21.2.

**Table 21.2: install Command-Line Options**

| Option | Argument | Description |
| :----- | :------- | :---------- |
| -g     | group    | Sets the group ownership on files to the GID or group name specified in group. The default GID is that of the parent process calling install. |
| -o     | owner    | Sets the ownership of files to the UID or user name specified in owner. The default owner is root. |
| -m     | mode     | Sets the file mode (permissions) to the octal or symbolic value specified in mode. The default file mode is 755, or read/write/execute for owner and read/execute for group and other. |

To specify dest as a directory, use the following syntax:

```
$ install -d [option[...]] dir[... ]
```

The -d switch instructs install to create the directory dir, including any parent directories, using any of the attributes listed in Table 21.2 or the default attributes.

### Examples

![](img/be588b36b489136ce784030a08a1d3d4_493_0.png)

#### Example

1. This example is taken from gdbm's makefile, the GNU database library. After expanding some of the make variables, the install target is

```
install: libgdbm.a gdbm.h gdbm.info
install -c -m 644 libgdbm.a $(libdir)/libgdbm.a
install -c -m 644 gdbm.h $(includedir)/gdbm.h
install -c -m 644 $(srcdir)/gdbm.info $(infodir)/gdbm.info
```

The make variables libdir, includedir, sccdir, and infodir are, respectively, /usr/lib, /usr/include, /usr/src/build/info, and /usr/info. So, libgdbm.a and gdbm.h will be read/write for the root user and read-only for everyone else. The file libgdbm.a gets copied to /usr/lib; gdbm.h, the header, winds up in /usr/include. The Texinfo file, gdbm.info, gets copied from /usr/src/build/info to /usr/info/gdbm.info. install overwrites existing files of the same name. The -c option is included for compatibility
