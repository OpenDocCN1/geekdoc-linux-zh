one of the original UNIX utilities for compressing files. A file compressed using `compress` generally has a .Z extension.

# Updating tar Files

So, now you have a nicely packaged and compressed tarball. But, suddenly, you realize you neglected to include the documentation. You did write documentation, didn’t you? Never fear, you can easily add new files to (or update existing files in) the tarball using tar’s `append` or `update` options.

To append your newly written documentation to the compressed tarball we created at the end of the last series of examples, you can use the `r` option or the `u` option. The r instructs tar to append the specified files to the end of the tarball. u, on the other hand, simply updates a file presently in the archive with a newer version. Naturally, if it does not exist in the archive, it will be added.

![](bbox=[0.03, 0.3, 0.12, 0.37])

# Example

This command uses `u` to update files with newer copies.

```
$ tar uvf mytar.tar /etc/*,conf
```

The output is identical to that generated when you created the tarball, so it is not repeated here. Note that the command did not use the compression option, z. This is because GNU tar, at least as of version 1.12, cannot update compressed files. As a result, it was necessary to uncompress the tarball first, using `gunzip mytar.tar`.

# Deleting Files from Tarballs

To delete a file from a tarball, you have to use the long option `--delete` and specify the name of the files you want to delete. As with the update option, you cannot delete files from a compressed tarball.

![](bbox=[0.03, 0.63, 0.12, 0.7])

# Example

This example deletes `isapp.conf` and `host.conf` from the tarball created in earlier examples.

```
$ tar --delete -f=mytar.tar isapp.conf host.conf
```

Note that the file deletion operation does not have a convenient single letter option; you *must* use `--delete`.

# Using the install Command

Consider `install` a `cp` command on steroids. In addition to copying files, it sets their permissions and, if possible, their owner and group. It can also create destination directories if they do not already exist.