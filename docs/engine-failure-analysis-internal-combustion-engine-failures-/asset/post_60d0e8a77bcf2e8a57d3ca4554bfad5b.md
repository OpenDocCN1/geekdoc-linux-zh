
124 Linux Command Instant Reference

## EXAMPLES

| This Command | Does the Following |
| :--- | :--- |
| `find /home/suzanne -size +1000k` | Finds all the files in the specified directory (/home/suzanne) that are larger than 1,000 kilobytes. |
| `find /home/suzanne -user 'bryan'` | Finds all the files in the specified directory (/home/suzanne) that are owned by the user named bryan. |
| `find -name 'proposal.txt' -exec less '{}' ';'` | Finds **proposal.txt** and displays the file using the **less** command (see Chapter 8). |
| `find -amin +5 -amin -10` | Finds all the files in the current directory that were last accessed 5 or more minutes ago but less than 10 or fewer minutes ago. |
| `find / -name '*.doc' -ctime -24` | Searches the entire filesystem to find all the files with the extension **.doc** that have been created or altered in the past 24 hours. |
| `find -name '*.doc' -ctime -24 -print0 \| xargs -0 cp /home/suzanne/backup` | Locates all the files in the current directory with the **.doc** extension that were created or altered in the past 24 hours and copies them to /home/suzanne/backup (see **xargs**). |
| `find / -name '*.doc' -print0 \| xargs -0 grep -l proposal` | Search the entire filesystem for files with the **.doc** extension that contain the word **proposal** (see **xargs** and **grep** in Chapter 8). |

## free

`free [ option ]`

Displays the following figures (in kilobytes) concerning available RAM memory: total memory available, memory currently in use, free memory, shared memory, memory used by kernel buffers, cached memory, size of the swap file, swap file currently in use, and free swap file.

### OPTIONS

| Use This Option | To Do This |
| :--- | :--- |
| `-b` | Display memory sizes in bytes instead of in kilobytes |
| `-k` | Display memory sizes in kilobytes (default) |
| `-m` | Display memory sizes in megabytes |
| `-o` | Do not display the buffer adjusted line |
| `-s n` | Check memory use every n seconds |
| `-t` | Display a line of totals at the bottom of the output |
| `-V` | Show the current version number |

### EXAMPLES

| This Command | Does the Following |
| :--- | :--- |
| `free` | Shows available and used memory in kilobytes. |
| `free -m` | Shows available and used memory in megabytes. |
| `free -mot` | Shows available and used memory in megabytes, hides the buffer adjusted line, and displays a line of totals at the bottom. |

## hcd

```
hcd directory
```

Changes directories in a mounted Macintosh (HFS) filesystem (see hmount in Chapter 7). This command is part of the macutils package, which can be downloaded at ftp://sunsite.unc.edu/pub/Linux/distributions/debian/source/otherosfs.

See also hdir, hls, hmkdir, hpwd, hmdir.

## hdir

```
hdir [ directory ]
```

Displays the contents of a directory in a mounted Macintosh (HFS) filesystem (see **hmount** in Chapter 7). This command is equivalent to hls with the `-1` option. It is part of the macutils package, which can be downloaded at `ftp://sunsite.unc.edu/pub/Linux/distributions/debian/source/otherosfs`.

See also hcd, hpwd.

## hls

```
hls [ option ] [ directory ]
```

Displays the contents of a directory in a mounted Macintosh (HFS) filesystem (see **hmount** in Chapter 7). This command is part of the macutils package, which can be downloaded at `ftp://sunsite.unc.edu/pub/Linux/distributions/debian/source/otherosfs`.

See also hdir, hpwd.

### OPTIONS

| Use This Option | To Do This |
| :--- | :--- |
| `-1` | Display the output line-by-line. |
| `-a` | Show all files and directories, including invisible ones. |
| `-b` | Display special characters with escape (backslash) notation rather than with a question mark. |
| `-c` | Sort entries by file creation date rather than by file modification date. |
| `-C` | Display entries in columnar format with entries sorted vertically. |
| `-d` | List directory entries but not their contents. |
| `-f` | Do not sort directory contents. |
| `-F` | Show type of entry. Directories are followed by a colon. Applications are followed by an asterisk. |
| `-I` | Show the catalog IDs for each entry. |
| `-l` | Display the entries in long format. |
| `-m` | Display the entries in a comma-separated list. |
| `-N` | Display filenames verbatim without escape characters or question marks. |
| `-q` | Replace special and non-printable characters with question marks (default). |
| `-Q` | Enclose all filenames in double quotation marks. |
| `-r` | Show entries in reverse order. |
| `-R` | Show contents of the working directory and all associated subdirectories (recursive display). |
| `-s` | Display file sizes in 1K units. |
| `-t` | Sort entries by the time of the last modification instead of by name. |
| `-U` | Do not sort directory contents. |
| `-w n` | Set the output width to *n* characters. |
| `-x` | Display entries in columnar format, sorted horizontally by rows. |

## hmkdir

`hmkdir [ directory ]`

Creates a directory in a mounted Macintosh (HFS) filesystem. This command is part of the macutils package, which can be downloaded at ftp://sunsite.unc.edu/pub/Linux/distributions/debian/source/otherosfs.

See also hmdir, hmount (Chapter 7).

## hpwd

`hpwd`

Displays the full path to the current directory in a mounted Macintosh (HFS) filesystem (see `hmount` in Chapter 7). This command is part of the macutils package, which can be downloaded at `ftp://sunsite.unc.edu/pub/Linux/distributions/debian/source/otherosfs`.

*See also* `hcd`, `hdir`, `hls`, `hmkdir`, `hmdir`.

## hmdir

`hmdir [ directory ]`

Removes an empty directory in a mounted Macintosh (HFS) filesystem. This command is part of the macutils package, which can be downloaded at `ftp://sunsite.unc.edu/pub/Linux/distributions/debian/source/otherosfs`.

*See also* `hmkdir`, `hmount` (Chapter 7).

## locate

`locate [ option ] [ shell pattern ]`

Quickly locates files by searching a database of filenames rather than the actual directory tree. To create the database, use `locatedb`. Unlike `slocate`, `locate` is not secure because it enables users to view files belonging to other users. For this reason, most distributions now provide `locate` and symbolically link this command to its newer, more secure alternative. By default, `locate` uses a substring search, so it is not necessary to use wildcards to search for one or more files that contain the specified shell pattern in their filenames. Note that the database does not reflect filesystem changes that have occurred since the system administrator last updated the database. You can use `cron` (see Chapter 12) to update the database automatically at specified intervals.

*See also updatedb.*

**NOTE** On most Linux distributions, **locate** is a symbolic link to **slocate**, which is a more secure version of this program. Try typing **slocate** at the command prompt to determine whether the more secure version is installed. If so, ignore the command syntax and options discussed here; see **slocate** instead.

### OPTIONS

| Use This Option | To Do This |
| :--- | :--- |
| `-u` | Create the **locate** database starting at the root directory (/). You must be logged in as the root user to use this option. |
| `-U directory` | Create the **locate** database starting at the specified directory. You must be logged in as the root user to use this option. |
| `-e directory1,directory2,...` | Exclude the specified directories from the **locate** database. You must be logged in as the root user to use this option. |
| `-f type` | Exclude the specified file system type (such as msdos or vfat) from the **locate** database. You must be logged in as the root user to use this option. |
| `-l < 0 \| 1 >` | Specify the security level: `0` Turns security checks off. `1` Turns security checks on (default). |
| `-n n` | Limit the number of results displayed to n (an integer). |
| `q` | Hide nonessential messages. |
| `-r regular expression` | Search the database using the specified regular expression. |
