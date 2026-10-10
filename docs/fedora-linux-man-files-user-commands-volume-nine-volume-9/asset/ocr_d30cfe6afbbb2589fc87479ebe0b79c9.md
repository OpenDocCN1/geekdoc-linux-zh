destination files against the —\*\*link\*\*-dest files can cause so paths in the destination to beco linked together due to the —\*\*link\*\*-dest associations.

Note that rsync can only detect hard links between files that are inside the transfer set. If rsync updates a file that has extra hard-link connections to files outside the transfer, that linkage will be broken. If you are tempted to use the \*\*inplace\*\* option to avoid this breakage, be very careful that you know how your files are being updated so that you are certain that no unintended changes happen due to lingering hard links (and see the \*\*inplace\*\* option for more caveats). If incremental recursion is active (see \*\*recursive\*\*), rsync may transfer a missing hard-linked file before it finds that another link for that contents exists elsewhere in the hierarchy. This does not affect the accuracy of the transfer (i.e. which files are hard-linked together), just its efficiency (i.e. copying the data for a new, early copy of a hard-linked file that could have been found later in the transfer in another set of the hard-linked set of files). One way to avoid this inefficiency is to disable incremental recursion using the \*\*no\-inc\-recursive\*\* option. \*\*perm\*\*s This option causes the receiving rsync to set the destination permissions to be the sa as the source permissions. (See also the \*\*chmod\*\* option for a way to modify what rsync considers to be the source permissions.) When this option is off, permissions are set as follows:

+   - o    Existing files (including updated files) retain their existing permissions, though the \*\*executability\*\* option might change just the execute permission for the file.
+   - o    New files get their "normal" permission bits set to the source file's permissions masked with the receiving directory's default permissions (either the receiving process's umask, or the permissions specified via the destination directory's default ACL), and their special permission bits disabled except in the case where a new directory inherits a setgid bit from its parent directory.

Thus, when \*\*perm\*\*s and \*\*executability\*\* are both disabled, rsync's behavior is the sa as that of other file-copy utilities, such as (1) and (1). In summary: to give destination files (both old and new) the source permissions, use \*\*perm\*\*s. To give new files the destination-default permissions (while leaving existing files unchanged), make sure that the \*\*perm\*\*s option is off and use \*\*chmod\*\*=ugo=rwX (which ensures that all non-masked bits get enabled). If you'd care to make this latter behavior easier to type, you could define a port alias for it, such as putting this line in the file \~/.port (the following defines the \*\*Z\*\* option, and includes \*\*no\*\* to use the default group of the destination dir):

```
rsync\ alias\ \-Z\ \-no\-p\ \-no\-g\ \-chmod\=ugo\=rwX
```

You could then use this new option in a command such as this one:

```
rsync\ \-avZ\ src/\ dest/
```

(Caveat: make sure that \*\*a\*\* does not follow \*\*Z\*\*, or it will re-enable the two "\*\*no\*\*" options ntioned above.) The preservation of the destination's setgid bit on newly-created directories when \*\*perm\*\*s is off was added in rsync 2.6.7. Older rsync versions erroneously preserved the three special permission bits for newly-created files when \*\*perm\*\*s was off, while overriding the destination's setgid bit setting on a newly-created directory. Default ACL observance was added to the ACL patch for rsync 2.6.7, so older