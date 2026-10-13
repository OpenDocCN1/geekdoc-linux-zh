
## CHMOD

- `-R, --recursive`—Changes files and directories recursively
- `--help`—Displays this help and exits
- `--version`—Outputs version information and exits

Each MODE is one or more of the letters `ugoa`, one of the symbols `+`, `-`, `=`, and one or more of the letters `rwxXstugo`.

### REPORTING BUGS

Report bugs to `<bug-fileutils@gnu.org>`.

### SEE ALSO

The full documentation for chmod is maintained as a Texinfo manual. If the `info` and `chmod` programs are properly installed at your site, the command

```
info chmod
```

should give you access to the complete manual.

## CHOWN

### NAME

`chown`—Change file owner and group.

### SYNOPSIS

```
chown [OPTION]... OWNER[.[GROUP]] FILE...
chown [OPTION]... .GROUP FILE...
chown [OPTION]... --reference=RFILE FILE...
```

### DESCRIPTION

This manual page documents the GNU version of chown. chown changes the user or group ownership of each given file, according to its first non-option argument, which is interpreted as follows. If only a username (or numeric user ID) is given, that user is made the owner of each given file, and the file’s group is not changed. If the username is followed by a colon or dot and a group name (or numeric group ID), with no spaces between, the group ownership of the files is changed as well. If a colon or dot but no group name follows the username, that user is made the owner of the files and the group of the files is changed to that user’s login group. If the colon or dot and group are given, but the username is omitted, only the group of the file is changed; in this case, chown performs the same function as chgrp.

### OPTIONS

Change the owner and/or group of each FILE to OWNER and/or GROUP.

- `-c, --changes`—Is verbose whenever change occurs
- `--dereference`—Affects the referent of each symbolic link, rather than the symbolic link itself
- `-h, --no-dereference`—Affects symbolic links instead of any referenced file (available only on systems that can change the ownership of a symlink)
- `-f, --silent, --quiet`—Suppresses most error messages
- `--reference=RFILE`—Uses the owner and group of RFILE instead of using explicit OWNER.GROUP values
- `-R, --recursive`—Operates on files and directories recursively
- `-v, --verbose`—Explains what is being done
- `--help`—Displays this help and exits
- `--version`—Outputs version information and exits

Owner is unchanged if missing. Group is unchanged if missing, but changed to login group if implied by a period. A colon can replace the period.

### REPORTING BUGS

Report bugs to `<bug-fileutils@gnu.org>`.

### SEE ALSO

The full documentation for chown is maintained as a Texinfo manual. If the `info` and `chown` programs are properly installed at your site, the command

```
info chown
```

should give you access to the complete manual.

## CP

### NAME

`cp`—Copy files and directories.

### SYNOPSIS

```
cp [OPTION]... SOURCE DEST
cp [OPTION]... SOURCE... DIRECTORY
```

### DESCRIPTION

- Copy SOURCE to DEST, or multiple SOURCE(s) to DIRECTORY.
- `-a, --archive` — Same as `-dpR`
- `-b, --backup` — Makes backup before removal
- `-d, --no-dereference` — Preserves links
- `-f, --force` — Removes existing destinations, never prompt
- `-i, --interactive` — Prompts before overwrite
- `-l, --link` — Links files instead of copying
- `-p, --preserve` — Preserves file attributes if possible
- `-P, --parents` — Appends source path to DIRECTORY
- `-r` — Copies recursively, non-directories as files
- `--sparse=WHEN` — Controls creation of sparse files
- `-R, --recursive` — Copies directories recursively
- `-s, --symbolic-link` — Makes symbolic links instead of copying
- `-S, --suffix=SUFFIX` — Overrides the usual backup suffix
- `-u, --update` — Copies only when the SOURCE file is newer than the destination file or when the destination file is missing
- `-v, --verbose` — Explains what is being done
- `-V, --version-control=WORD` — Overrides the usual version control
- `-x, --one-file-system` — Stays on this file system
- `--help` — Displays this help and exits
- `--version` — Outputs version information and exits

By default, sparse SOURCE files are detected by a crude heuristic method and the corresponding DEST file is made sparse as well. That is the behavior selected by `--sparse=auto`. Specify `--sparse=always` to create a sparse DEST file whenever the SOURCE file contains a long enough sequence of zero bytes. Use `--sparse=never` to inhibit creation of sparse files.

The backup suffix is ~, unless set with SIMPLE_BACKUP_SUFFIX. The version control can be set with VERSION_CONTROL. Values are:

- `t`, numbered — make numbered backups
- `nil`, existing — numbered if numbered backups exist, simple otherwise
- `never`, simple — always make simple backups

As a special case, cp makes a backup of SOURCE when the force and backup options are given and SOURCE and DEST are the same name for an existing, regular file.

### REPORTING BUGS

Report bugs to `<bug-fileutils@gnu.org>`.

### SEE ALSO

The full documentation for cp is maintained as a Texinfo manual. If the `info` and `cp` programs are properly installed at your site, the command

```
info cp
```

should give you access to the complete manual.

## CRONTAB

### NAME

`crontab`—Maintain crontab files for individual users (V3).

### SYNOPSIS

```
crontab [ -u user ] file
crontab [ -u user ] { -l | -r | -e }
```

### DESCRIPTION

crontab is the program used to install, uninstall or list the tables used to drive the cron(8) daemon in Vixie Cron. Each user can have his own crontab, and though these are files in /var, they are intended to be edited directly.

If the *allow* file exists, you must be listed therein to be allowed to use this command. If the *allow* file does not exist but the *deny* file does exist, you must not be listed in the deny file in order to use this command. If neither of these files exists then depending on site-dependent configuration parameters, only the super-user will be allowed to use this command, or all users will be able to use this command.

If the -u option is given, it specifies the name of the user whose crontab is to be tweaked. If this option is not given, crontab examines your crontab, that is, the crontab of the person executing the command. Note that su(8) can confuse crontab and that if you are running inside of su(8) you should always use the -u option for safety’s sake.

The first form of this command is used to install a new crontab from some named file or standard input if the pseudo-filename ‘-’ is given.

The -l option causes the current crontab to be displayed on standard output.

The -r option causes the current crontab to be removed.

The `-e` option is used to edit the current crontab using the editor specified by the VISUAL or EDITOR environment variables. After you exit from the editor, the modified crontab will be installed automatically.

### SEE ALSO

`crontab(5)`, `cron(8)`

### FILES

- `/etc/cron.allow`
- `/etc/cron.deny`

### STANDARDS

The crontab command conforms to IEEE Std1003.2-1992 (‘POSIX’). This new command syntax differs from previous versions of Vixie Cron, as well as from the classic SVR3 syntax.

### DIAGNOSTICS

A fairly informative usage message appears if you run it with a bad command line.

### AUTHOR

Paul Vixie `paul@vix.com`

## DF

### NAME

`df` — Report file system disk space usage.

### SYNOPSIS

```
df [OPTION]... [FILE]...
```

### DESCRIPTION

This manual page documents the GNU version of `df`. `df` displays the amount of disk space available on the file system containing each filename argument. If no filename is given, the space available on all currently mounted file systems is shown. Disk space is shown in 1K blocks by default unless the environment variable POSIXLY_CORRECT is set, in which case 512-byte blocks are used.

If an argument is the absolute filename of a disk device node containing a mounted file system, `df` shows the space available on that system rather than on the file system containing the device node (which is always the root file system). This version of `df` cannot show the space available on unmounted file systems because on most kinds of systems, doing so requires very nonportable intimate knowledge of file system structures.
