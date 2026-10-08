# Finding Suspicious Files

```
; find ! -ftype proc -perm +6000 \
-print xargs -n 50 md5sum) \
- sort tee want_su
```

The following command will find these set-UID and set-GID files and report differences from the previous search:

```
(find / ! -ftype proc -perm +6000 -ls \
; find / ! -ftype proc -perm +6000 \
-print xargs -n 50 md5sum) \
- sort diff want_su \
Mail -s 'SU changed' admin@yourite.com
```

The diff technique used here also be applied to the rest of the file commands described below or throughout the book. It is not shown in the examples for simplicity.

The following example will show world-writable files. Expect to see /tmp and a few other directories and device files.

```
find / ! -ftype proc -perm -2 -type | -ls
```

Files whose start with dot (".") are not listed by ls and crackers will have their file names with dot to hide them. As you know, the startup scripts for various programs frequently start with a dot so that commands on users' home directories will not produce excessive interesting output. The -a flag causes ls to list these too, of course.) You could use find clauses of the form

```
! -name .profile ! -name .chshrc -name .login
```

before the -ls or -exec action clauses to ignore shell files. This would allow a cracker to hide data in these file names. Even ignoring them only in users' home directories is not completely safe because most users run only a single type of shell

```
find / ! -ftype proc '(' -name .??* -o -name '[.]' ')' -ls
```

The following command will find files whose numeric UID (owner) is not in /etc/passwd whose numeric GID is not in /etc/group. This could have resulted from someone extracting a tar archive legitimately or from an incomplete cleanup of a removed user. Also, they could be from a cracker extracting a tar archive containing a Rootkit or another evil utility. Many of the previous commands will find will generate lots of false positives, everything that one finds should be investigated and corrected.

```
find / ! -ftype proc '(' -nouser -o -nroup ')' -ls
```