# ALPHABETICAL COMMAND REFERENCE 481

be sorted or use the option -o. sort does not deal accurately with foreign languagenspecial characters.

# Example

```
user$ ls -l | sort +2
```

sorts the contents list passed by user and group names. Files with identical user group names are sorted by size.

```
split [options] file [target.file]
```

split divides the specified file into several files. Depending on the selected option, the source file is split every n bytes, Kbytes or files. When no target file is specified, the command produces the files xaa, xab, and so on. When a target file is specified, this file name followed by the character combinations aa, ab, and so on is used for the resulting file names.

+   -n n or -l --lines=n
split the source file into single files of n lines each.

+   -b n or --bytes=n
split the source file every n bytes. The letters k or m, when specified after n stand for Kbytes or Mbytes.

+   -C n or --line-bytes=n
same -b, but the files are split at the end of lines and are therefore in most cases a few bytes smaller than n.

# Examples

```
user split -c 1430 backup.tar disk.
```

splits the archive file backup.tar into single files of 1430 Kbytes each and names them.aa, disk.ab, and so on. These files can be stored on diskettes.

```
user cat disk. * > total.tar
```

combines the single files back into one complete file.

```
su [options] [user]
```

su (substitute user) without options changes into root mode without the laborious login and login (but obviously with password input). Thus, root becomes the active user until the next exit command.

Optionally, a different user than the default user root can be specified with su. when it is executed by root, it is not even necessary to enter a password when changing users.

+   -l or --login
at the change of users, all login files are read. This is required for a proper configuration of PATH.