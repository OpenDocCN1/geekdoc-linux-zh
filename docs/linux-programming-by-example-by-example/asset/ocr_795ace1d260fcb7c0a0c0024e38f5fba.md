# Invoking tar

In its simplest form, the command to create a tarball is

```
$ tar cf archivename filelist
```

`c` says to create a tarball from the files indicated by `filelist`. `f` says to name the tarball `archivename`. You will generally want to compress the tarball to conserve disk space and minimize download time. The easiest way to do so, using GNU's `tar`, is to add `z` to the option list, which causes `tar` to invoke another GNU utility, `gzip`, on the tarball to compress it. In this case, the invocation would look like the following:

```
$ tar czf archivename filelist
```

![](bbox=[0.04, 0.29, 0.14, 0.35])

# Examples

+   1. The following `tar` invocation creates a tarball named `mytar.tar` from all the files in the `/etc` directory that end in `.conf`:

![](bbox=[0.04, 0.44, 0.14, 0.49])

# Output

```
$ tar cf mytar.tar /etc/*.conf
tar: Cannot add file /etc/amd.conf: Permission denied
tar: Removing leading '/' from absolute path names in the archive
tar: Cannot add file /etc/quota.conf: Permission denied
tar: Error exit delayed from previous errors
```

You might get errors because mortal users do not have access to certain files. In this case, `tar` will not add that file to the archive, but otherwise the archive will still be created.

![](bbox=[0.04, 0.64, 0.14, 0.69])

# Example

+   2. To list the contents of the archive, use the following command:

![](bbox=[0.04, 0.75, 0.14, 0.8])

# Output