
talking to an older rsync. See also `--delete-delay` and `--delete-after`.

**--delete-before**
Request that the file-deletions on the receiving side be done before the transfer starts. See `--delete` (which is implied) for more details on file-deletion. Deleting before the transfer is helpful if the filesystem is tight for space and removing extraneous files would help to make the transfer possible. However, it does introduce a delay before the start of the transfer, and this delay might cause the transfer to timeout (if `--timeout` was specified). It also forces rsync to use the old, non-incremental recursion algorithm that requires rsync to scan all the files in the transfer into memory at once (see `--recursive`).

**--delete-during**, `--del`
Request that the file-deletions on the receiving side be done incrementally as the transfer happens. The per-directory delete scan is done right before each directory is checked for updates, so it behaves like a more efficient `--delete-before`, including doing the deletions prior to any per-directory filter files being updated. This option was first added in rsync version 2.6.4. See `--delete` (which is implied) for more details on file-deletion.

**--delete-delay**
Request that the file-deletions on the receiving side be computed during the transfer (like `--delete-during`), and then removed after the transfer completes. This is useful when combined with `--delay-updates` and/or `--fuzzy`, and is more efficient than using `--delete-after` (but can behave differently, since `--delete-after` computes the deletions in a separate pass after all updates are done). If the number of removed files overflows an internal buffer, a temporary file will be created on the receiving side to hold the names (it is removed while open, so you shouldn't see it during the transfer). If the creation of the temporary file fails, rsync will try to fall back to using `--delete-after` (which it cannot do if `--recursive` is doing an incremental scan). See `--delete` (which is implied) for more details on file-deletion.

**--delete-after**
Request that the file-deletions on the receiving side be done after the transfer has completed. This is useful if you are sending new per-directory rule files as a part of the transfer and you want their exclusions to take effect for the delete phase of the current transfer. It also forces rsync to use the old, non-incremental recursion algorithm that requires rsync to scan all the files in the transfer into memory at once (see `--recursive`). See `--delete` (which is implied) for more details on file-deletion.

**--delete-excluded**
In addition to deleting the files on the receiving side that are not on the sending side, this tells rsync to also delete any files on the receiving side that are excluded (see `--exclude`). See the FILTER RULES section for a way to make individual exclusions behave this way on the receiver, and for a way to protect files from `--delete-excluded`. See `--delete` (which is implied) for more details on file-deletion.

**--ignore-missing-args**
When rsync is first processing the explicitly requested source files (e.g. command-line arguments or `--files-from` entries), it is normally an error if the file cannot be found. This option suppresses that error, and does not try to transfer the file. This does not affect subsequent vanished-file errors if a file was initially found to be present and later is no longer there.

**--delete-missing-args**
This option takes the behavior of (the implied) `--ignore-missing-args` option a step further: each missing arg will become a deletion request of the corresponding destination file on the receiving side (should it exist). If the destination file is a non-empty directory, it will only be successfully deleted if `--force` or `--delete` are in effect. Other than that, this option is independent of any other type of delete processing. The missing source files are represented by special file-list entries which display as a "*missing" entry in the `--list-only` output.

**--ignore-errors**
Tells `--delete` to go ahead and delete files even when there are I/O errors.

**--force**
This option tells rsync to delete a non-empty directory when it is to be replaced by a non-directory. This is only relevant if deletions are not active (see `--delete` for details). Note for older rsync versions: `--force` used to still be required when using `--delete-after`, and it used to be non-functional unless the `--recursive` option was also enabled.

**--max-delete=NUM**
This tells rsync not to delete more than NUM files or directories. If that limit is exceeded, all further deletions are skipped through the end of the transfer. At the end, rsync outputs a warning (including a count of the skipped deletions) and exits with an error code of 25 (unless some more important error condition also occurred). Beginning with version 3.0.0, you may specify `--max-delete=0` to be warned about any remaining files in the destination without removing any of them. Older clients interpreted this as “unlimited”, so if you don’t know what version the client is, you can use the less obvious `--max-delete=-1` as a backward-compatible way to specify that no deletions are allowed (though really old versions didn’t warn when the limit was exceeded).

**--max-size=SIZE**
This tells rsync to avoid transferring any file that is larger than the specified SIZE. The SIZE value can be suffixed with a string to indicate a size multiplier, and may be a fractional value (e.g. `--max-size=1.5m`). This option is a transfer rule, not an exclude, so it doesn’t affect the data that goes into the file-lists, and thus it doesn’t affect deletions. It just limits the files that the receiver requests to be transferred. The suffixes are as follows: “K” (or “KiB”) is a kibibyte (1024), “M” (or “MiB”) is a mebibyte (1024*1024), and “G” (or “GiB”) is a gibibyte (1024*1024*1024). If you want the multiplier to be 1000 instead of 1024, use “KB”, “MB”, or “GB”. (Note: lower-case is also accepted for all values.) Finally, if the suffix ends in either “+1” or “-1”, the value will be offset by one byte in the indicated direction. Examples: `--max-size=1.5-1` is 1499999 bytes, and `--max-size=2g+1` is 2147483649 bytes. Note that rsync versions prior to 3.1.0 did not allow `--max-size=0`.

**--min-size=SIZE**
This tells rsync to avoid transferring any file that is smaller than the specified SIZE, which can help in not transferring small, junk files. See the `--max-size` option for a description of SIZE and other information. Note that rsync versions prior to 3.1.0 did not allow `--min-size=0`.

**-B**, **--block-size=BLOCKSIZE**
This forces the block size used in rsync’s delta-transfer algorithm to a fixed value. It is normally selected based on the size of each file being updated. See the technical report for details.

**-e**, **--rsh=COMMAND**
This option allows you to choose an alternative remote shell program to use for communication between the local and remote copies of rsync. Typically, rsync is configured to use ssh by default, but you may prefer to use rsh on a local network. If this option is used with `[user@]host::module/path`, then the remote shell `COMMAND` will be used to run an rsync daemon on the remote host, and all data will be transmitted through that remote shell connection, rather than through a direct socket connection to a running rsync daemon on the remote host. See the section “USING RSYNC-DAEMON FEATURES VIA A REMOTE-SHELL CONNECTION” above. Command-line arguments are permitted in `COMMAND` provided that `COMMAND` is presented to rsync as a single argument. You may use spaces (not tabs or other whitespace) to separate the command and args from each other, and you can use single- and/or double-quotes to preserve spaces in an argument (but not backslashes). Note that doubling a single-quote inside a single-quoted string gives you a single-quote; likewise for double-quotes (though you need to pay attention to which quotes your shell is parsing and which quotes rsync is parsing). So examples:

- `-e 'ssh -p 2234'`
- `-e 'ssh -o "ProxyCommand nohup ssh firewall nc -w1 %h %p"'`

(Note that ssh users can alternately customize site-specific connect options in their .ssh/config file.) You can also choose the remote shell program using the RSYNC_RSH environment variable, which accepts the same range of values as -e. See also the `--blocking-io` option which is affected by this option.

**--rsync-path=PROGRAM**
Use this to specify what program is to be run on the remote machine to start-up rsync. Often used when rsync is not in the default remote-shell’s path (e.g., `rsync-path=/usr/local/bin/rsync`). Note that PROGRAM is run with the help of a shell, so it can be any program, script, or command sequence you’d care to run, so long as it does not corrupt the standard-in & standard-out that rsync is using to communicate. One tricky example is to set a different default directory on the remote machine for use with the `--relative` option. For instance:

```
rsync -avR -e "cd a/b; rsync" host:c/d e/
```

**-M**, **--remote-option=OPTION**
This option is used for more advanced situations where you want certain effects to be limited to one side of the transfer only. For instance, if you want to pass `--log-file=FILE` and `--fake-super` to the remote system, specify it like this:

```
rsync -av -M -log-file=foo -M -fake-super src/ dest/
```

If you want to have an option affect only the local side of a transfer when it normally affects both sides, send its negation to the remote side. Like this:

```
rsync -av -x -M-no-x src/ dest/
```

Be cautious using this, as it is possible to toggle an option that will cause rsync to have a different idea about what data to expect next over the socket, and that will make it fail in a cryptic fashion. Note that it is best to use a separate `--remote-option` for each option you want to pass. This makes your usage compatible with the `--protect-args` option. If that option is off, any spaces in your remote options will be split by the remote shell unless you take steps to protect them. When performing a local transfer, the “local” side is the sender and the “remote” side is the receiver. Note that some versions of the popt option-parsing library have a bug in them that prevents you from using an adjacent arg with an equal in it next to a short option letter (e.g. `-M-log-file=/tmp/foo`). If this bug affects your version of popt, you can use the version of popt that is included with rsync.

**-C**, **-cvs-exclude**
This is a useful shorthand for excluding a broad range of files that you often don’t want to transfer between systems. It uses a similar algorithm to CVS to determine if a file should be ignored. The exclude list is initialized to exclude the following items (these initial items are marked as perishable — see the FILTER RULES section):

- `RCS`
- `SCCS`
- `CVS`
- `CVSroot`
- `RCSlog`
- `cvslog`
- `*.v`
- `tags`
- `TAGS`
- `*.make.state`
- `*.nse_dep_end*`
- `*.lib`
- `*.o`
- `*.a`
- `*.obj`
- `*.so`
- `*.exe`
- `*.Z`
- `*.elc`
- `*~`
- `core`
- `.svn/`
- `.git/`
- `.hg/`
- `.bzr/`

then, files listed in a `$HOME/.cvsignore` are added to the list and any files listed in the `CVSIGNORE` environment variable (all `cvsignore` names are delimited by whitespace). Finally, any file is ignored if it is in the same directory as a `.cvsignore` file and matches one of the patterns listed therein. Unlike rsync’s filter/exclude files, these patterns are split on whitespace. See the `cvs(1)` manual for more information. If you’re coining -C with your own
