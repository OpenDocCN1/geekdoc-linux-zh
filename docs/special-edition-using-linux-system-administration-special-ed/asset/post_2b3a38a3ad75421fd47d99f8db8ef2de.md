
## TESTS

- `-perm +mode`—Any of the permission bits mode are set for the file.
- `-regex pattern`—Filename matches regular expression pattern. This is a match on the whole path, not a search. For example, to match a file named `./fubar3`, use the regular expression `.*bar.` or `.*b.*3`, but not `b.*r3`.
- `-size n[bckw]`—File uses n units of space. The units are 512-byte blocks by default or if b follows n, bytes if c follows n, kilobytes if k follows n, or 2-byte words if w follows n. The size does not count indirect blocks, but does count blocks in sparse files that are not actually allocated.
- `-true`—Always true.
- `-type c`—File is of type c:
  - `b`—Block (buffered) special.
  - `c`—Character (unbuffered) special.
  - `d`—Directory.
  - `p`—Named pipe (FIFO).
  - `f`—Regular file.
  - `l`—Symbolic link.
  - `s`—Socket.
- `-uid n`—File's numeric user ID is n.
- `-used n`—File was last accessed n days after its status was last changed.
- `-user uname`—File is owned by user uname (numeric user ID allowed).
- `-xtype c`—The same as `-type` unless the file is a symbolic link. For symbolic links: if `-follow` has not been given, true if the file is a link to a file of type c; if `-follow` has been given, true if c is l. In other words, `-xtype` checks the type of the file that `-type` does not check.

## ACTIONS

- `-exec command ;`—Execute command; true if 0 status is returned. All following arguments to `find` are taken to be arguments to the command until an argument consisting of `;` is encountered. The string `{}` is replaced by the current filename being processed everywhere it occurs in the arguments to the command, not just in arguments where it is alone, as in some versions of `find`. Both these constructions might need to be escaped (with a `\`) or quoted to protect them from expansion by the shell. The command is executed in the starting directory.
- `-fls file`—True; like `-ls` but write to file like `-fprint`.
- `-fprint file`—True; print the full filename into file file. If file does not exist when `find` is run, it is created; if it does exist, it is truncated. The filenames `/dev/stdout` and `/dev/stderr` are handled specially; they refer to the standard output and standard error output, respectively.
- `-fprint0 file`—True; like `-print0` but write to file like `-fprint`.
- `-fprintf file format`—True; like `-printf` but write to file like `-fprint`.
- `-ok command ;`—Like `-exec` but ask the user first (on the standard input); if the response does not start with ‘y’ or ‘Y’, do not run the command, and return false.
- `-print`—True; print the full filename on the standard output, followed by a new line.
- `-print0`—True; print the full filename on the standard output, followed by a null character. This allows filenames that contain new lines to be correctly interpreted by programs that process the find output.
- `-printf format`—True; print format on the standard output, interpreting `\\` escapes and `%` directives. Field widths and precisions can be specified as with the `printf` C function. Unlike `-print`, `-printf` does not add a new line at the end of the string. The escapes and directives are:
  - `\a`—Alarm bell
  - `\b`—Backspace
  - `\c`—Stop printing from this format immediately and flush the output
  - `\f`—Form feed
  - `\n`—Newline
  - `\r`—Carriage return
  - `\t`—Horizontal tab
  - `\v`—Vertical tab
  - `\\`—A literal backslash (`\`)

A `\` character followed by any other character is treated as an ordinary character, so they both are printed.

  - `%%`—A literal percent sign.
  - `%a`—File’s last access time in the format returned by the C `ctime` function.
  - `%Ak`—File’s last access time in the format specified by `k`, which is either `@` or a directive for the C `strftime` function. The possible values for `k` are listed in the following text; some of them might not be available on all systems, due to differences in `strftime` between systems.
    - `@`—Seconds since Jan. 1, 1970, 00:00 GMT
    - Time fields:
      - `H`—Hour (00..23)
      - `I`—Hour (01..12)
      - `k`—Hour ( 0..23)
      - `l`—Hour ( 1..12)
      - `M`—Minute (00..59)
      - `p`—locale’s AM or PM
      - `r`—time, 12-hour (hh:mm:ss [AP]M)
      - `s`—Second (00..61)
      - `T`—Time, 24-hour (hh:mm:ss)
      - `x`—Locale’s time representation (H:M:S)
      - `z`—Time zone (for example, EDT), or nothing if no time zone is determinable
    - Date fields:
      - `a`—Locale’s abbreviated weekday name (Sun..Sat)
      - `A`—Locale’s full weekday name, variable length (Sunday..Saturday)
      - `b`—Locale’s abbreviated month name (Jan..Dec)
      - `B`—Locale’s full month name, variable length (January..December)
      - `c`—Locale’s date and time (Sat Nov 04 12:02:33 EST 1989)
      - `d`—Day of month (01..31)
      - `D`—Date (mm/dd/yy)
      - `h`—Same as b
      - `j`—Day of year (001..366)
      - `m`—Month (01..12)
      - `u`—Week number of year with Sunday as first day of week (00..53)
      - `w`—Day of week (0..6)
      - `W`—Week number of year with Monday as first day of week (00..53)
      - `x`—Locale’s date representation (mm/dd/yy)
      - `y`—Last two digits of year (00..99)
      - `Y`—Year (1970...)
  - `%b`—File’s size in 512-byte blocks (rounded up).
  - `%c`—File’s last status change time in the format returned by the C `ctime` function.
  - `%Ck`—File’s last status change time in the format specified by k, which is the same as for `%A`.
  - `%d`—File’s depth in the directory tree; 0 means the file is a command line argument.
  - `%f`—File’s name with any leading directories removed (only the last element).
  - `%F`—The type of the file system the file is on; this value can be used for `-fstype`.
  - `%g`—File’s group name, or numeric group ID if the group has no name.
  - `%G`—File’s numeric group ID.
  - `%h`—Leading directories of file’s name (all but the last element).
  - `%H`—Command-line argument under which file was found.
  - `%i`—File’s inode number (in decimal).
  - `%k`—File’s size in 1K blocks (rounded up).
  - `%l`—Object of symbolic link (empty string if file is not a symbolic link).
  - `%m`—File’s permission bits (in octal).
  - `%n`—Number of hard links to file.
  - `%p`—File’s name.
  - `%P`—File’s name with the name of the command-line argument under which it was found removed.
  - `%s`—File’s size in bytes.
  - `%t`—File’s last modification time in the format returned by the C `ctime` function.
  - `%Tk`—File’s last modification time in the format specified by `k`, which is the same as for `%A`.
  - `%u`—File’s username, or numeric user ID if the user has no name.
  - `%U`—File’s numeric user ID.

A `%` character followed by any other character is discarded (but the other character is printed).

- `-prune`—If `-depth` is not given, true; does not descend the current directory. If `-depth` is given, false; no effect.
- `-ls`—True; list current file in `ls -dils` format on standard output. The block counts are of 1K blocks unless the environment variable `POSIXLY_CORRECT` is set, in which case 512-byte blocks are used.

## OPERATORS

Listed in order of decreasing precedence:

- `( expr )`—Force precedence
- `! expr`—True if `expr` is false
- `-not expr`—Same as `! expr`
- `expr1 expr2`—And (implied); `expr2` is not evaluated if `expr1` is false
- `expr1 -a expr2`—Same as `expr1 expr2`
- `expr1 -and expr2`—Same as `expr1 expr2`
- `expr1 -o expr2`—Or; `expr2` is not evaluated if `expr1` is true
- `expr1 -or expr2`—Same as `expr1 -o expr2`
- `expr1 , expr2`—List; both `expr1` and `expr2` are always evaluated. The value of `expr1` is discarded; the value of the list is the value of `expr2`.

## SEE ALSO

`locate(1L)`, `locatedb(5L)`, `updatedb(1L)`, `xargs(1L)`

Finding Files (online in Info, or printed)

## GREP

### NAME

grep, egrep, fgrep—Print lines matching a pattern.

### SYNOPSIS

```
grep [-[AB] NUM] [-[CEFGVbchilnqsvwx]] [-e PATTERN] [-f FILE] [-d ACTION]
[--directories=ACTION] [--extended-regexp] [--fixed-strings] [--basic-regexp]
[--regexp=PATTERN] [--file=FILE] [--ignore-case] [--word-regexp] [--line-regexp]
[--no-messages] [--revert-match] [--version] [--help] [--byte-offset]
[--line-number] [--with-filename] [--no-filename] [--quiet] [--silent] [--text]
[--files-without-match] [--files-with-matches] [--count] [--before-context=NUM]
[--after-context=NUM] [--context] [--binary] [--unix-byte-offsets] [--recursive]
files...
```

### DESCRIPTION

grep searches the named input *files* (or standard input if no files are named, or the filename `-` is given) for lines containing a match to the given *pattern*. By default, grep prints the matching lines.

Three major variants of grep are controlled by the following options:

- `-G`, `--basic-regexp`—Interpret pattern as a basic regular expression (see the following). This is the default.
- `-E`, `--extended-regexp`—Interpret pattern as an extended regular expression (see the following).
- `-F`, `--fixed-strings`—Interpret pattern as a list of fixed strings, separated by newlines, any of which are to be matched.

In addition, two variant programs, egrep and fgrep, are available. egrep is similar (but not identical) to grep -E, and is compatible with the historical UNIX egrep. fgrep is the same as grep -F.

All variants of grep understand the following options:

- `-A NUM`, `--after-context=NUM`—Print NUM lines of trailing context after matching lines.
- `-B NUM`, `--before-context=NUM`—Print NUM lines of leading context before matching lines.
- `-C`, `--context[=NUM]`—Print NUM lines (default 2) of output context.
- `-NUM`—Same as `--context=NUM` lines of leading and trailing context. However, grep will never print any given line more than once.
