# 1382

The following example tries to recognize the archive's actual blocking factor, using a
ninal blocking factor that is too small.

```
castle tar tvf /dev/rmt/0 10
tar: tape read error
```

# Environment Variables

SYS3 Override the default behavior of tar and provide compatibility with
INTERACTIVE UNIX systems and SCO UNIX installation scripts. Do
not use this environment variable in new scripts; it is intended for
compatibility only. When set, the following options behave differently.

+   -F filename Use filename to obtain a list of command-line
itches and on which to operate.

+   -e Prevent files from splitting across volumes. If there
isufficient room on one volume, prompt for a new
volume. If the file does not fit on the new volume,
with an error.

See environ(5) for descriptions of the following environment variables that affect the
execution of tar: LC_TYPE, LC_MESSAGES, LC_TIME, TZ, and NLPATH.

# Exit Status

+   0 Successful completion.
>0 An error occurred.

# Files

```
/dev/rmt/[0-7] [b] [n]
/dev/rmt/[0-7]1[b] [n]
/dev/rmt/[0-7]m[b] [n]
/dev/rmt/[0-7]h[b] [n]
/dev/rmt/[0-7]u[b] [n]
/dev/rmt/[0-7]c[b] [n]
/etc/default/tar
```

Settings may look like this:

```
archive0=/dev/rmt/0
archive1=/dev/rmt/0n
archive2=/dev/rmt/1
archive3=/dev/rmt/1n
archive4=/dev/rmt/0
archive5=/dev/rmt/0n
archive6=/dev/rmt/1
archive7=/dev/rmt/1n
```