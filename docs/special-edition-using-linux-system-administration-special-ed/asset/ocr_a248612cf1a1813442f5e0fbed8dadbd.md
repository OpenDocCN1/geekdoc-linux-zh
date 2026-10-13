```
```
#       The numbers represent the amount of the original file the
#       compressed file is expected to take up.
#       Default: [compress 0.50, 0.50]
#   compress - specify compression of the backed up data. Valid
#       values are:
#       "none"        - don't compress the dump output.
#       "client best" - compress on the client using the best
#                       (and probably slowest) algorithm.
#       "client fast" - compress on the client using fast
#                       algorithm.
#       "server best" - compress on the tape host using the best
#                       (and probably slowest) algorithm.
#       "server fast" - compress on the tape host using a fast
#                       algorithm. This may be useful when a fast
#                       tape host is backing up slowly.
#       Default: [compress client fast]
#   dumpcycle - set the number of days in the dump cycle, ie, set
#       how often a full dump should be performed.
#       Default: from DUMPCYCLE above
#   exclude - specify files and directories to be excluded from
#       the dump. Useful with gnutar only; silently ignored by dump
#       and samba.
#       Valid values are:
#       "pattern"    - a shell glob pattern defining which files
#                       to exclude.
#                       gnutar gets --exclude="pattern"
#       list "filename" - a file (on the client) containing
#       patterns
#                       re's (1 per line) defining which files to
#                       exclude.
#                       gnutar gets --exclude-from="filename"
#       Note that the full pathname of a file with its
#       filesystem starts with './', because of the way amanda runs
#       gnutar: `tar -C $mountpoint -cf - --files-from .`
#       (note the final dot!) Thus, if you're backing up '/usr'
#       with a diskfile entry like 'host /usr gnutar-root', but
#       you don't want to backup /usr/tmp, your exclude list should
#       contain the pattern './tmp', as this is relative to the
#       '/usr' above. Please refer to the man-page of gnutar for
#       more information.
#       Default: include all files
#
#   holdingdisk   - should the holding disk be used for this
#       dump. Useful for dumping the holding disk itself.
#       Default: [holdingdisk yes]
#   ignore - do not back this filesystem up. Useful for sharing a
#       single disklist in several configurations.
#   index  - keep an index of the files backed up.
#       Default: [index no]
#   kencrypt - encrypt the data stream between the client and
#       server.
#       Default: [kencrypt no]
#   maxdumps - max number of concurrent dumps to run on the client.
#       Default: [maxdumps 1]
#   priority - priority level of the dump. Valid levels are "low",
#       "medium", or "high". These are really only used when
#       Amanda has no tape to write to because of some error. In
```
```