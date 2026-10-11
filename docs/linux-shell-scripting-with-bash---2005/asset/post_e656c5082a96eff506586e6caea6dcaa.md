
Lines unaffected by `sed` can be hidden with the `~quiet` (or `~n` or `~silent`) switch.

Like the `transform` command, there are other `sed` commands that mimic Linux commands. The `p` (print) command imitates the `grep` command by printing a matching line. This is useful only when the `~quiet` switch is used. The `~` (line number) command prints the line number of matching lines. The `q` (quit) command makes `sed` act like the `head` command, displaying lines until a certain line is encountered.

```
$ head orders.txt | sed -quiet '/^$B/p'\
Bunk Bed,705.99,1,757\
Queen Bed,925.99,1,757\
\
$ head orders.txt | sed -quiet '/^$B/d'\
5\
6
```

The remaining `sed` commands represent specialized actions. The flow of control is handled by the `n` (next) command. Files can be read with `r` or written with `w`. `a` (append next) combines two lines into one for matching purposes. `d` (multiple line delete) deletes multiple lines. `p` is multiple line print. `h`, `H`, `g`, `G`, and `x` enable you to save lines to a temporary buffer so that you can make changes, display the results, and then restore the original text for further analysis. This works like an electronic calculator's memory. Complicated `sed` expressions can feature branches to labels embedded in the expressions using the `b` command. The `t` (test) command acts as a `shell if` or `switch` statement, attempting a series of operations until one succeeds. Subcommands can be embedded in `sed` with curly brackets. More documentation on these commands can be found using `info sed`.

Long `sed` scripts can be stored in a file. You can read the `sed` script from a file with the `~files` (or `~f`) switch. You can include comments with a `#` character, like a `shell` script.

`sed` expressions can also be specified using the `~expression` (or `~e`) switch, or can be read from standard input when a `~filename` is used.

You cannot use `ASCII` value escape sequences in `sed` patterns.

## Compressing Files

Most Linux programs differentiate between archiving and compression. *Archiving* is the storage of a number of files into a single file. *Compression* is a reduction of file size by encoding the file. In general, an archive file takes up more space than the original files, so most archive files are also compressed.

The Linux `bzip2` (BWH zip) command compresses files with Burrows–Wheeler–Huffman compression. This is the most commonly used compression format. Older compression programs are available on most distributions. `gzip` (GNU zip) compresses with `LZ77` compression and is used extensively on older distributions. `compress` is an older Lempel–Ziv compression program available on most versions of `Unix`. `zip` is the Linux version of the DOS `pkzip` program. `hexbin` decompresses certain Macintosh archives.

The **Linux tar** (*tape archive*) command is the most commonly used archiving command, and it automatically compresses while archiving when the right command-line options are used. Although the command was originally used to collect files for storage on tape drives, it can also create disk files.

Originally, the **tar** command didn't use command-line switches: A series of single characters were used. The Linux version supports command-line switches as well as the older single character syntax for backward compatibility.

To use **tar** on files, the `--file` (*F* (or *-f*)) switch indicates the filename to act on. At least one action switch must be specified to indicate what **tar** will do with the file. Remote files can be specified with a preceding hostname and a colon.

The `--create` (*-c*) switch creates a new tar file.

```
$ ls -1 orders.txt
-rw-rw-r--  1 kburcht  kburcht     592 May 11 14:45 orders.txt
$ tar --create --file orders.tar orders.txt
$ ls -1 orders.tar
-rw-rw-r--  1 kburcht  kburcht   10240 Oct  3 12:06 orders.tar
```

The archive file is significantly larger than the original file. To apply compression, choose the type of compression using `--bzip` (or *-I*), `--gzip` (or *-z*), `--compress` (or *-Z*), or `--use-compress-program` to specify a particular compression program.

```
$ tar --create --file orders.tbz --bzip orders.txt
$ ls -1 orders.tbz
-rw-rw-r--  1 kburcht  kburcht     421 Oct  3 12:12 orders.tbz
$ tar --create --file orders.tgz --gzip orders.txt
$ ls -1 orders.tgz
-rw-rw-r--  1 kburcht  kburcht     430 Oct  3 12:11 orders.tgz
```

More than one file can be archived at once.

```
$ tar --create --file orders.tbz --bzip orders.txt orders2.txt
$ ls -1 orders.tbz
-rw-rw-r--  1 kburcht  kburcht     502 Oct  3 12:14 orders.tbz
```

The new archive overwrites an existing one.

To restore the original files, use the `--extract` switch. Use `--verbose` to see the filenames. **tar** cannot auto-detect the compression format; you must specify the proper compression switch to avoid an error.

```
$ tar --extract --file orders.tbz
tar: 502 garbage bytes ignored at end of archive
tar: Error exit delayed from previous errors
$ tar --extract --bzip --file orders.tbz
$ tar --extract --verbose --bzip --file orders.tbz
orders.txt
orders2.txt
```

The `--extract` switch also restores any subdirectories in the pathname of the file. It's important to extract the files in the same directory where they were originally compressed to ensure they are restored to their proper places.

The `tar` command can also append files to the archive using `--concatenate` (or `-A`), compare to archives with `--compare` (or `--diff` or `-d`), remove files from the archive with `--delete`, list the contents with `--list`, and replace existing files with `--update`. `tar` silently performs these functions unless `--verbose` is used.

A complete list of `tar` switches appears in the reference section.

Another archiving program, `cpio` (*copy in/out*) is provided for compatibility with other flavors of `Unix`. The `rpm` package manager command is based on `cpio`.

## Reference Section

### `grep` Command Switches

- `--after-context=n` (or `-A n`)—Prints `n` lines following the matching line
- `--before-context=n` (or `-B n`)—Prints `n` lines prior to a matching line
- `--context[=n]` (or `-C [n]`)—Displays `n` lines (default is 2) around the matching line
- `--basic-regexp` (or `-G`)—Pattern is not an extended regular expression
- `--binary-files=binary`—Normal binary file behavior; issues a message if the pattern is somewhere in a binary file
- `--binary-files=without-match` (or `-I`)—`grep` assumes all binary files don't match
- `--binary-files=text` (or `-a` or `--text`)—Shows matches from binary files
- `--byte-offset` (or `-b`)—Prints the byte offset within the input file before each line of output
- `--count` (or `-c`)—Prints a count of matching lines for each input file
- `--directories=read` (or `-d read`)—`grep` uses its normal behavior, reading the directory as if it were a normal file
- `--directories=skip` (or `-d skip` or `-x`)—Directories are ignored
- `--directories=recurse` (or `-d recurse` or `-r` or `--recursive`)—Examines files in all subdirectories
- `-fixed-strings` (or `-F`)—Treats the pattern as a string, ignoring any special meaning to the characters
- `-invert-match` (or `-v`)—Selects lines that do not match the pattern
- `-no-filename` (or `-h`)—Hides the filenames with each match
- `-line-number` (or `-n`)—Shows the line number with results
- `-line-regexp` (or `-x`)—Matches only an entire line
- `-mmap`—Uses memory mapping to speed up search on a file that won't shrink while grep is running
- `-no-messages` (or `-s`)—Suppresses error messages about missing files
- `-null` (or `-Z`)—Separates items with null characters instead of a carriage return
- `-quiet` (or `-q`)—Searches only to the first match and doesn't display it
- `-regexp=P` (or `-E P`)—Use string P as the matching pattern, useful for patterns starting with a period
- `-with-filename` (or `-H`)—Prints the filename with each match
- `-word-regexp` (or `-w`)—Only matches whole “words” separated from the rest of the line by spaces or other non-word characters

### `find` Command Switches

There are a large number of `find` expression switches. They include the following:

- `-empty`—Matches an empty regular file or directory
- `-false`—Always fails to match
- `-fstype FS`—The file must be on a file system of type FS
- `-gid N`—Matches numeric group ID N
- `-group N`—The file must be owned by this group ID. The group ID can be a name or number
- `-daystart`—Measures times from the start of the day rather than 24 hours ago
- `-depth`—Find the contents of a directory before the directory itself (a depth-first traversal)
- `-file FILE`—Writes `-ls` results to specified file
- `-follow`—Follows symbolic links. Normally, links are not followed
- `-fprint F`—Writes `-print` results to file F
- `-fprint0 F`—Writes `-print0` results to file F
- `-fprintf F FORMAT`—Writes `-printf` results to file F
- `-mindepth N`—Descends at least N directories from the current directory
- `-ilname pattern`—Case-insensitive `-lname`
