
# ALPHABETICAL COMMAND REFERENCE 447

-a or --archive
preserves all attributes of the file. -a is an abbreviation for -dpR

-b or --backup
already existing files are not overwritten, renamed as backup files (file plus -)

-d or --dereference
only copies a link, but not the file pointed to by the link.

-i or --interactive
asks for confirmation before overwriting existing files.

-l or --link
creates hard links instead of copying the files. When cp is used with this option,
it has the same functionality as ln (see page 463).

-p or --preserve
leaves information about owner, group membership, access rights and the date
and time of last modification unchanged. Without this option, the copy belongs
to the user who executes cp (user and group), and the date and time are set to
the current date and time.

-R or --recursive
copies all subdirectories and the files they contain.

-s or --symbolic-link
creates symbolic links instead of copying the files or directories. With this option,
cp has the same functionality as ln -s (see 463).

-u or --update
copies files only if this does not cause a homonymous file with a more recent
date to be overwritten.

Another command suited to copying whole directory trees (especially
between different hard disk partitions) is tar (see page 483).

Example

```
user cp book/*.tex
```

* all *.tex files from the subdirectory into the current directory, which in
the above command is named by a single dot.

# cpio [options] [pattern]

cpio combines several files into an archive and copies them to another storage
medium (for example, to a streamer) or to another directory. Similarly, the command
also can be used to read such data. Under Linux, cpio is not widely used; tar
is more popular. The greatest advantage of cpio is that voluminous archives are
automatically distributed out (and read back from) from several data supports (similar
to the DOS programs BACKUP and RESTORE).

cpio is, for example, needed for the installation of programs which have been
recorded by their manufacturers on diskettes or tapes using cpio. The three central
cpio commands are:

-o (output) for storing data. The files are combined into one archive and written to the standard output.

-i (input) for reading archived data.

-p (pass through) for the transfer of archives between different directories.

These three main commands can be controlled through various options. Details can be found in the man pages.

# csplit [options] file split.position

csplit splits a file at predetermined positions into several single files. The split position can be specified either directly by a number of lines or a search pattern. As a result, the command produces files xx00, xx01, and so on, and displays their lengths on screen. Through the specification of appropriate options, 'prettier' file names can be generated. The cat command can be used to combine these single files back into the original file. (See also split on page 481 for splitting files of any type — binary—smaller files of n bytes each.)

# Specification of the split positions

The split positions are specified either as a number of lines or a search pattern. In the first case, the file is split after n lines, in the second case or before the occurrence of the search pattern. When csplit is used to split the file several times (which is normally the case), the number of times the operation is to be repeated must be the number of lines or the split pattern.

- +n splits the file after n lines.

- /pattern/ splits the file after the line preceding the occurrence of the pattern. (The line which contains the pattern becomes the first line of the next file.)

- /pattern/+n splits the line after (+) or before (-) the occurrence of the pattern.

- {n} splits the file into n+1 files (not just into two).

# Options

- -f file or --prefix=file uses the specified filename to name the output files.

- -k or --keep-files already created files are not deleted when an error occurs. This option must always be used with pattern specifications of the form n (*). Patterns are specified as grep.

-z or --elide-empty-files
prevents the creation of empty files. Without this option, empty files can occur.
especially when the first line of the source file matches the search pattern.

# Examples

```
user csplit -k f part.total.txt 100 (*)
```

splits total.txt into the files part.00, part.01, and so on. Each file is 100 long.

```
user csplit -k f part.total.txt '/^% ---/-' (*)
```

as above, except that the file is split every time a line begins with the text ---

# cut [options] file

cut extracts the columns specified by the options from each line of a text.

- -b list
extracts the characters specified in a list. Single characters may be separated by commas (but not by spaces). Alternatively, entire ranges can be specified, such as -b 3-6,9,11-15.

- -f list --fields
as above, but applying to fields (data records) which must be separated by tab characters.

- -d --delimiter character
specifies the separation character for -f; this character is to be used instead of tab character.

- -s or --only-delimited
eliminates all lines that do not contain data that corresponds to the -f option. Cannot be used together with -b.

# Example

```
ls -l | cut -b 1-11,56-
```

uses cut to filter the list obtained with ls. As a result, only the access rights and the file names (characters 1 to 11 and all characters from the 56th character onwards) are displayed.

# date [options] time

date displays the current date and time or changes them. (Changes can only be carried by root.) date can display the time in various formats (see the man texts).

- -s sets the date and/or time (instead of displaying them).

# dd [options]

dd transfers data between different storage media (hard disk, diskette, and so on), and if required, carries out a data conversion. The command can be used to exchange data between different computer architectures.

dd can not copy single files, but also accesses devices directly. This can be used to copy entire hard disks (or partitions), modify the boot sector of a hard disk, and so on. There is no need to create a file system on the hard disk or diskette.

When dd is used without options, it reads the data from the standard input (keyboard, terminated by Ctrl+Z) and writes to the standard output (screen). Please note that the options of dd must be specified without preceding minus signs!

```
conv=mode
```

converts the data during the copying process. There exist various settings for mode, such as case (upper case into lower case letters), ucase (lower case into upper case), swap (swaps 2 bytes at a time), and so on.

```
bs=n
```

specifies the block size for input and output files. (The block size determines how many bytes are read or written at once.)

```
count=n
```

copies n blocks (not all data).

```
ibs=n
```

specifies the block size of the source file.

```
if=source.file
```

specifies the source file (instead of the standard input).

```
obs=n
```

specifies the block size of the target file.

```
of=target.file
```

specifies the target file (instead of standard output).

# Examples

```
user dd if=/dev/hda of=/bootsector.bak bs=512 count=1
```

transfers the boot sector of first IDE disk.

```
user dd if=/vmlinux of=/dev/fd0
```

copies the kernel directly into diskette, which can then be used as.

# df [options]

df provides information about the directory tree where hard disks (partitions) or other drives are mounted and how much free storage is available on each.

# ALPHABETICAL COMMAND REFERENCE 451

-i or --inodes
instead of the free storage in Kbytes, information is displayed about.

# diff [options] file1 file2

diff compares two text files. The result is a list of all lines that differ from another. The command is relatively "intelligent", that is, when lines have been added in one file, only this fact is signalled. Subsequent lines are again recognized as identical, although their line numbers are different. Thus, this program can be effectively used to quickly document the differences between two versions of a program.

- -b regards multiple spaces and empty lines as single spaces/lines.

- -w completely ignores spaces and empty lines.

# dmesg

Messages displayed by the kernel during the boot process can be viewed at a later stage by dmesg. Such kernel messages can, for example, help determine which hardware has been recognized. Depending on the setting in /etc/syslog.conf, kernel messages are also stored in /var/log/messages
The texts of the Init-V process (page 124) displayed after the boot process are not stored and therefore cannot be viewed with dmesg. Some programs or so-called daemons, however, write their logs or error messages into various //log/xxx files.

# du [options] [directory]

du provides information about the storage used by files or directories. When a file specification is given in the directory parameter (for example *.txt), it provides a list showing the sizes of all files. When only a directory is specified, it calculates the storage used by all subdirectories. The sizes include the storage used by all subdirectories. The last figure indicates the total storage used by all files and subdirectories below the specified directory. All sizes are given in Kbytes.

- -b or --bytes
indicates the sizes in bytes (instead of Kbytes).

- -c or --total
displays the total space as the last value. This option is only needed when du is applied to files (and not to directories). With this option, it is easy to determine how much space is occupied by all files with a given extension (for example *.txt).

- -s or --summarize
displays only the total space. This option only makes sense when the storage of directories is shown.
