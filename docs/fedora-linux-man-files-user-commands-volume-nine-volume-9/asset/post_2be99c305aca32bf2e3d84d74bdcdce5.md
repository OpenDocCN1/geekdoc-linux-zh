
## rsync Options

**`--compare-dest=DIR`**
directory). If a file is found in *DIR* that is identical to the sender's file, the file will NOT be transferred to the destination directory. This is useful for creating a sparse backup of just files that have changed from an earlier backup. This option is typically used to copy into an empty (or newly created) directory. Beginning in version 2.6.4, multiple `--compare-dest` directories may be provided, which will cause rsync to search the list in the order specified for an exact match. If a match is found that differs only in attributes, a local copy is made and the attributes updated. If a match is not found, a basis file from one of the *DIRs* will be selected to try to speed up the transfer. If *DIR* is a relative path, it is relative to the destination directory. See also `--copy-dest` and `--link-dest`. NOTE: beginning with version 3.1.0, rsync will remove a file from a non-empty destination hierarchy if an exact match is found in one of the compare-dest hierarchies (making the end result more closely match a fresh copy).

**`--copy-dest=DIR`**
This option behaves like `--compare-dest`, but rsync will also copy unchanged files found in *DIR* to the destination directory using a local copy. This is useful for doing transfers to a new destination while leaving existing files intact, and then doing a flash-cutover when all files have been successfully transferred. Multiple `--copy-dest` directories may be provided, which will cause rsync to search the list in the order specified for an unchanged file. If a match is not found, a basis file from one of the *DIRs* will be selected to try to speed up the transfer. If *DIR* is a relative path, it is relative to the destination directory. See also `--compare-dest` and `--link-dest`.

**`--link-dest=DIR`**
This option behaves like `--copy-dest`, but unchanged files are hard linked from *DIR* to the destination directory. The files must be identical in all preserved attributes (e.g. permissions, possibly ownership) in order for the files to be linked together. An example:

```
rsync -av --link-dest=$PWD/prior_dir host:src_dir/ new_dir/
```

If file's aren't linking, double-check their attributes. Also check if so attributes are getting forced outside of rsync's control, such as a mount option that squishes root to a single user, or mounts a removable drive with generic ownership (such as OS X's "Ignore ownership on this volume" option). Beginning in version 2.6.4, multiple `--link-dest` directories may be provided, which will cause rsync to search the list in the order specified for an exact match. If a match is found that differs only in attributes, a local copy is made and the attributes updated. If a match is not found, a basis file from one of the *DIRs* will be selected to try to speed up the transfer. This option works best when copying into an empty destination hierarchy, as existing files may get their attributes tweaked, and that can affect alternate destination files via hard-links. Also, itemizing of changes can get a bit muddled. Note that prior to version 3.1.0, an alternate-directory exact match would never be found (nor linked into the destination) when a destination file already exists. Note that if you combine this option with `--ignore-times`, rsync will not link any files together because it only links identical files together as a substitute for transferring the file, never as an additional check after the file is updated. If *DIR* is a relative path, it is relative to the destination directory. See also `--compare-dest` and `--copy-dest`. Note that rsync versions prior to 2.6.1 had a bug that could prevent `--link-dest` from working properly for a non-super-user when -0 was specified (or implied by -a). You can work-around this bug by avoiding the -o option when sending to an old rsync.

**`-z`, `--compress`**
With this option, rsync compresses the file data as it is sent to the destination machine, which reduces the amount of data being transmitted — something that is useful over a slow connection. Note that this option typically achieves better compression ratios than can be achieved by using a compressing remote shell or a compressing transport because it takes advantage of the implicit information in the matching data blocks that are not explicitly sent over the connection. This matching-data compression comes at a cost of CPU, though, and can be disabled by repeating the -z option, but only if both sides are at least version 3.1.1. Note that if your version of rsync was compiled with an external zlib (instead of the zlib that comes packaged with rsync) then it will not support the old-style compression, only the new-style (repeated-option) compression. In the future this new-style compression will likely become the default. The client sync requests new-style compression on the server via the **new-compress** option, so if you see that option rejected it means that the server is not new enough to support -zz. Rsync also accepts the **old-compress** option for a future time when new-style compression becomes the default. See the **skip-compress** option for the default list of file suffixes that will not be compressed.

**`compress-level=NUM`**
Explicitly set the compression level to use (see **compress**) instead of letting it default. If NUM is non-zero, the **compress** option is implied.

**`skip-compress=LIST`**
Override the list of file suffixes that will not be compressed. The LIST should be one or more file suffixes (without the dot) separated by slashes (/). You may specify an empty string to indicate that no file should be skipped. Simple character-class matching is supported: each must consist of a list of letters inside the square brackets (e.g. no special classes, such as “[:alpha:],” are supported, and ‘*’ has no special meaning). The characters asterisk (*) and question-mark (?) have no special meaning. Here’s an example that specifies 6 suffixes to skip (since 1 of the 5 rules matches 2 suffixes):

- `-skip-compress=gz/jpg/mp[34]/7z/bz2`

The default list of suffixes that will not be compressed is this (in this version of rsync): 7z ace avi bz2 deb gpg gz iso jpeg jpg lz lzma lzo mov mp3 mp4 ogg png rar rpm rzip tbz tgz tlz txz xz z zip

This list will be replaced by your **skip-compress** list in all but one situation: a copy from a daemon rsync will add your skipped suffixes to its list of non-compressing files and its list may be configured to a different default).

**`numeric-ids`**
With this option rsync will transfer numeric group and user IDs rather than using user and group names and mapping them at both ends. By default rsync will use the username and groupname to determine what ownership to give files. The special uid 0 and the special group 0 are never mapped via user/group names even if the **numeric-ids** option is not specified. If a user or group has no name on the source system or it has no match on the destination system, then the numeric ID from the source system is used instead. See also the comments on the “use chroot” setting in the rsyncd.conf manual page for information on how the chroot setting affects rsync’s ability to look up the names of the users and groups and what you can do about it.

**`usermap=STRING`**, **`groupmap=STRING`**
These options allow you to specify users and groups that should be mapped to other values by the receiving side. The STRING is one or more FROM:TO pairs of values separated by commas. Any matching FROM value from the sender is replaced with a TO value from the receiver. You may specify usernames or user IDs for the FROM and TO values, and the FROM value may also be a wild-card string, which will be matched against the sender’s names (wild-cards do NOT match against ID numbers, though see below for why a ‘*’ matches everything). You may instead specify a range of ID numbers via an inclusive range: LOW-HIGH. For example:

- `usermap=0:99:nobody,wayne:admin,*:normal`
- `--groupmap=usr:1,1:usr`

The first match in the list is the one that is used. You should specify all your user mappings using a single `--usermap` option, and/or all your group mappings using a single `--groupmap` option. Note that the sender’s name for the 0 user and group are not transmitted to the receiver, so you should either match these values using a 0, or use the names in effect on the receiving side (typically “root”). All other **FROM** names match those in use on the sending side. All **TO** names match those in use on the receiving side. Any IDs that do not have a name on the sending side are treated as having an empty name for the purpose of matching. This allows them to be matched via a “*” or using an empty name. For instance:

- `--usermap=:nobody`
- `--groupmap=*:nobody`

When the `--numeric-ids` option is used, the sender does not send any names, so all the IDs are treated as having an empty name. This means that you will need to specify numeric **FROM** values if you want to map these nameless IDs to different values. For the `--usermap` option to have any effect, the **-o** (`--owner`) option must be used (or implied), and the receiver will need to be running as a super-user (see also the `--fake-super` option). For the `--groupmap` option to have any effect, the **-g** (`--groups`) option must be used (or implied), and the receiver will need to have permissions to set that group.

**`--chown=USER:GROUP`**
This option forces all files to be owned by USER with group GROUP. This is a simpler interface than using `--usermap` and `--groupmap` directly, but it is implemented using those options internally, so you cannot mix them. If either the USER or GROUP is empty, no mapping for the omitted user/group will occur. If GROUP is empty, the trailing colon may be omitted, but if USER is empty, a leading colon must be supplied. If you specify “`--groupmap=foo:bar`, this is exactly the same as specifying “`--usermap=*:foo --groupmap=*:bar`”, only easier.

**`--timeout=TIMEOUT`**
This option allows you to set a maximum I/O timeout in seconds. If no data is transferred for the specified time then rsync will exit. The default is 0, which means no timeout.

**`--contimeout`**
This option allows you to set the amount of time that rsync will wait for its connection to an rsync daemon to succeed. If the timeout is reached, rsync exits with an error.

**`--address`**
By default rsync will bind to the wildcard address when connecting to an rsync daemon. The `--address` option allows you to specify a specific IP address (or hostname) to bind to. See also this option in the `--daemon` mode section.

**`--port=PORT`**
This specifies an alternate TCP port number to use rather than the default of 873. This is only needed if you are using the double-colon (::) syntax to connect with an rsync daemon (since the URL syntax has a way to specify the port as a part of the URL). See also this option in the `--daemon` mode section.

**`--sockopts`**
This option can provide endless fun for people who like to tune their systems to the utmost degree. You can set all sorts of socket options which may make transfers faster (or slower!). Read the man page for the setsockopt() system call for details on some of the options you may be able to set. By default no special socket options are set. This only affects direct socket connections to a rsync daemon. This option also exists in the `--daemon` mode section.

**`--blocking-io`**
This tells rsync to use blocking I/O when launching a remote shell transport. If the remote shell is either rsh or remsh, rsync defaults to using blocking I/O, otherwise it defaults to using non-blocking I/O. (Note that ssh prefers non-blocking I/O.)

**`--obuf=MODE`**
This sets the output buffering mode. The mode can be None (aka Unbuffered), Line, or Block (aka Full). You may specify as little
