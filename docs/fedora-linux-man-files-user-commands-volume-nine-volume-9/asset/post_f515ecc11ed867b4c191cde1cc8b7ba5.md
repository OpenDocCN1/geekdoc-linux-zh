
options (e.g. `--no-D`, `--no-perms`) or have different defaults in various circumstances (e.g. `--no-whole-file`, `--blocking-io`, `--no-dirs`). You may specify either the short or the long option name after the "no" prefix (e.g. `-R` is the same as `--relative`).

For example: if you want to use `-a` (`-archive`) but don't want `-o` (`-owner`), instead of converting `-a` into `-rlptgD`, you could specify `-a -no-o` (or `-a -no-owner`).

The order of the options is important: if you specify `--no-r -a`, the `-r` option would end up being turned on, the opposite of `-a -no-r`. Note also that the side-effects of the `--files-from` option are NOT positional, as it affects the default state of several options and slightly changes the meaning of `-a` (see the `--files-from` option for more details).

## **-r**, **\-recursive**

This tells rsync to copy directories recursively. See also `--dirs` (`-d`).

Beginning with rsync 3.0.0, the recursive algorithm used is now an incremental scan that uses much less memory than before and begins the transfer after the scanning of the first few directories have been completed. This incremental scan only affects our recursion algorithm, and does not change a non-recursive transfer. It is also only possible when both ends of the transfer are at least version 3.0.0.

Some options require rsync to know the full file list, so these options disable the incremental recursion mode. These include: `--delete-before`, `--delete-after`, `--prune-empty-dirs`, and `--delay-updates`. Because of this, the default delete mode when you specify `--delete` is now `--delete-during` when both ends of the connection are at least 3.0.0 (use `--del` or `--delete-during` to request this improved deletion mode explicitly). See also the `--delete-delay` option that is a better choice than using `--delete-after`.

Incremental recursion can be disabled using the `--no-inc-recursive` option or its shorter `--no-i-r` alias.

## **-R**, **\-relative**

Use relative paths. This means that the full path names specified on the command line are sent to the server rather than just the last parts of the filenames. This is particularly useful when you want to send several different directories at the same time. For example, if you used this command:

`rsync -av /foo/bar/baz.c remote:/tmp/`

... this would create a file named baz.c in /tmp/ on the remote machine. If instead you used

`rsync -avR /foo/bar/baz.c remote:/tmp/`

then a file named /tmp/foo/bar/baz.c would be created on the remote machine, preserving its full path. These extra path elements are called "implied directories" (i.e. the "/foo" and the "/foo/bar" directories in the above example). Beginning with rsync 3.0.0, rsync always sends these implied directories as real directories in the file list, even if a path element is really a symlink on the sending side. This prevents some really unexpected behaviors when copying the full path of a file that you didn't realize had a symlink in its path. If you want to duplicate a server-side symlink, include both the symlink via its path, and referent directory via its real path. If you're dealing with an older rsync on the sending side, you may need to use the `--no-implied-dirs` option.

It is also possible to limit the amount of path information that is sent as implied directories for each path you specify. With a modern rsync on the sending side (beginning with 2.6.7), you can insert a dot and a slash into the source path, like this:

`rsync -avR /foo/. /bar/baz.c remote:/tmp/`

That would create /tmp/bar/baz.c on the remote machine. (Note that the dot must be followed by a slash, so '/foo/.' would not be abbreviated.) For older rsync versions, you would need to use a chdir to limit the source path. For example, when pushing files:

`(cd /foo; rsync -avR bar/baz.c remote:/tmp/)`

(Note that the parens put the two commands into a sub-shell, so that the ‘cd’ command doesn’t remain in effect for future commands.) If you’re pulling files from an older rsync, use this idiom (but only for a non-daemon transfer):

`rsync -avR --rsync-path="cd /foo; rsync" remote:bar/baz.c /tmp/`

**--no-implied-dirs** This option affects the default behavior of the `--relative` option. When it is specified, the attributes of the implied directories from the source names are not included in the transfer. This means that the corresponding path elements on the destination system are left unchanged if they exist, and any missing implied directories are created with default attributes. This even allows these implied path elements to have big differences, such as being a symlink to a directory on the receiving side. For instance, if a command-line arg or a files-from entry told rsync to transfer the file ‘path/foo/file’, the directories ‘path’ and ‘path/foo’ are implied when `--relative` is used. If ‘path/foo’ is a symlink to ‘bar’ on the destination system, the receiving rsync would ordinarily delete ‘path/foo’, recreate it as a directory, and receive the file into the new directory. With `--no-implied-dirs`, the receiving rsync updates ‘path/foo/file’ using the existing path element, which means that the file ends up being created in ‘path/bar’. Another way to accomplish this link preservation is to use the `--keep-dirlinks` option (which will also affect symlinks to directories in the rest of the transfer). When pulling files from an rsync older than 3.0.0, you may need to use this option if the sending side has a symlink in the path you request and you wish the implied directories to be transferred as normal directories.

**-b**, **--backup** With this option, preexisting destination files are renamed as each file is transferred or deleted. You can control where the backup file goes and what (if any) suffix gets appended using the `--backup-dir` and `--suffix` options. Note that if you don’t specify `--backup-dir`, (1) the `--omit-dir-times` option will be implied, and (2) if `--delete` is also in effect (without `--delete-excluded`), rsync will add a ‘protect’ filter-rule for the backup suffix to the end of all your existing excludes (e.g., `-f ‘P *~’`). This will prevent previously backed-up files from being deleted. Note that if you are supplying your own filter rules, you may need to manually insert your own exclude/protect rule somewhere higher up in the list so that it has a high enough priority to be effective (e.g., if your rules specify a trailing inclusion/exclusion of ‘*’, the auto-added rule would never be reached).

**--backup-dir=DIR** In combination with the `--backup` option, this tells rsync to store all backups in the specified directory on the receiving side. This can be used for incremental backups. You can additionally specify a backup suffix using the `--suffix` option (otherwise the files backed up in the specified directory will keep their original filenames). Note that if you specify a relative path, the backup directory will be relative to the destination directory, so you probably want to specify either an absolute path or a path that starts with “../”. If an async daemon is the receiver, the backup dir cannot go outside the module’s path hierarchy, so take extra care not to delete it or copy into it.

**--suffix=SUFFIX** This option allows you to override the default backup suffix used with the `--backup` (-b) option. The default suffix is a ~ if no `--backup-dir` was specified, otherwise it is an empty string.

**-u**, **--update** This forces rsync to skip any files which exist on the destination and have a modified time that is newer than the source file. (If an existing destination file has a modification time equal to the source file’s, it will be updated if the sizes are different.) Note that this does not affect the copying of dirs, symlinks, or other special files. Also, a difference of file format between the sender and receiver is always considered to be important enough for an update, no matter what date is on the objects. In other words, if the source has a directory where the destination has a file, the transfer would occur regardless of the timestamps. This option is a transfer rule, not an exclude, so it doesn’t affect the data that goes into the file-lists, and thus it doesn’t affect deletions. It just limits the files that the receiver requests to be transferred.

**--inplace** This option changes how rsync transfers a file when its data needs to be updated: instead of the default method of creating a new copy of the file and moving it into place when it is complete, rsync instead writes the updated data directly to the destination file. This has several effects:

- Hard links are not broken. This means the new data will be visible through other hard links to the destination file. Moreover, attempts to copy differing source files onto a tightly-linked destination file will result in a “tug of war” with the destination data changing back and forth.

- In-use binaries cannot be updated (either the OS will prevent this from happening, or binaries that attempt to swap-in their data will misbehave or crash).

- The file’s data will be in an inconsistent state during the transfer and will be left that way if the transfer is interrupted or if an update fails.

- A file that rsync cannot write to cannot be updated. While a super user can update any file, a normal user needs to be granted write permission for the open of the file for writing to be successful.

- The efficiency of rsync’s delta-transfer algorithm may be reduced if so much data in the destination file is overwritten before it can be copied to a position later in the file. This does not apply if you use `--backup`, since rsync is smart enough to use the backup file as the basis file for the transfer.

WARNING: you should not use this option to update files that are being accessed by others, so be careful when choosing to use this for a copy. This option is useful for transferring large files with block-based changes or appended data, and also on systems that are disk bound, not network bound. It can also help keep a copy-on-write filesystem snapshot from diverging the entire contents of a file that only has minor changes. The option implies `--partial` (since an interrupted transfer does not delete the file), but
