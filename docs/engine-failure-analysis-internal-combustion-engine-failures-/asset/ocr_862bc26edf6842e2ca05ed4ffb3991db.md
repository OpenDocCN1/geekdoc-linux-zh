# OPTIONS

| Use This Option | To Do This |
|---|---|
| `-b` | Display memory sizes in bytes instead of in kilobytes |
| `-k` | Display memory sizes in kilobytes (default) |
| `-m` | Display memory sizes in megabytes |
| `-o` | Do not display the buffer adjusted line |
| `-s n` | Check memory use every n seconds |
| `-t` | Display a line of totals at the bottom of the output |
| `-V` | Show the current version number |

# EXAMPLES

| This Command | Does the Following |
|---|---|
| `free` | Shows available and used memory in kilobytes. |
| `free -m` | Shows available and used memory in megabytes. |
| `free -mot` | Shows available and used memory in megabytes, hides the buffer adjusted line, and displays a line of totals at the bottom. |

# hcd

```
hcd directory
```

Changes directories in a mounted Macintosh (HFS) filesystem (see hmount in Chapter 7). This command is part of the macutils package, which can be downloaded at ftp://sunsite.unc.edu/pub/Linux/distributions/debian/source/otherosfs.

See also hdir, hls, hmkdir, hpwd, hmdir.