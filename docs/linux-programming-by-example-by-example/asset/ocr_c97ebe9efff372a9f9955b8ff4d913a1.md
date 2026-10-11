```
etc/smb.conf
etc/syslog.conf
```

Note that `tar` does not remove any of the original files, but merely creates a new tarball.

![](bbox=[0.04, 0.15, 0.12, 0.2])

# Example

+   3. To create a compressed archive, simply add `z` to the option list. Traditionally, compressed tarballs, usually called *gripped tarballs*, are named by adding `.gz` to the end. They are also often given the extension `.tgz`. Either one is acceptable. For purposes of consistency, this chapter will add `.gz` to the end of the filename.

![](bbox=[0.04, 0.34, 0.13, 0.39])

# Output

```
$ tar czvf mytar.tar.gz /etc/*.conf
etc/dosemu.conf
etc/gpm-root.conf
etc/host.conf
etc/inetd.conf
etc/isapnp.conf
etc/ld.so.conf
etc/lilo.conf
etc/logrotattar: Cannot add file /etc/quota.conf: Permission denied
tar: Error exit delayed from previous errors
smb.conf
etc/syslog.conf
```

The `v` option instructs `tar` to be verbose, that is, to list the files it is adding to the archive. Again, it is safe to ignore errors that occur due to file access violations.

> **TIP**
> Using the `z` option to compress a tarball slows down `tar`'s operation somewhat, but it saves typing because you do not have to issue a second shell command, using `gzip`, to compress the tarball. On the other hand, calling `gzip` directly results in much better compression, but you have to type an additional command to prepare your package for distribution. Because programmers are lazy critters, makefiles usually include a target named `dist` that creates a gzipped tarball. This reduces the amount of typing you'll have to do and is convenient: simply type `make dist` and your package is ready to upload for the rest of the world to download.

Make sure you understand the difference between `gzip`, `zip`, and `compress`. `gzip` is the standard file compression utility on Linux systems. It is also the default compression utility used when you use `tar`'s `z` option. Compressed archives created using `gzip` generally have a `.gz` extension on them. `zip` creates PKZIP compatible files but is a free alternative to the PKZIP utilities. Files compressed using `zip` have a `.zip` extension. `compress`, finally, is