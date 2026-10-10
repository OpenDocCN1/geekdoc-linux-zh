
## OPTIONS (CONT.)

| Use This Option | To Do This |
| --- | --- |
| -h, --dereference | Don't archive symbolic links; instead, archive the files they point to. |
| -l, --bzip2 | Use bzip2 for compression and decompression. |
| -i, --ignore-zeroes | Ignore blocks of zeroes in the archive. |
| --ignore-failed-read | Don't exit if an unreadable file is encountered. |
| -k, --keep-old-files | Don't overwrite existing files when restoring from the archive. |
| -K filename, --starting-file filename | Start with the specified filename in the archive. |
| -l, --one-file-system | Stay in the current filesystem. |
| -L n, --tape-length n | Change tapes after writing n kilobytes of data. |
| -m, --modification-time | Don't extract the file modification times. |
| -M, --multivolume | Work with a multivolume archive. |
| -N date, --after-date date, -newer date | Archive only the files that are newer than the specified date. |
| -O, --to-stdout | Extract files to the standard output. |
| -o, --old-archive, --portability | Write a V7 format archive rather than the default ANSI format. |
| -p, --same-permissions, --preserve-permissions | Keep the existing permissions. |
| -P, --absolute-paths | Don't remove path information from filenames. |
| -preserve | Same as -ps. |
| -R, --record-number | Display the record number in the archive. |
| --remove-files | Remove the files after adding them to the archive. |
| -s, --same-order, --preserve-order | Sort the list of names of files to extract to match the names in the archive. |
| --same-owner | Create extracted files with the same ownership. |
| -S, --sparse | Work with sparse files correctly. |
| -T filename, --files-from filename | Consult the specified filename for the names of files to extract. |
| --null | Read null-terminated names. |
| --totals | Display the total bytes written with `--create`. |
| -v, --verbose | Show the names of files being processed. |
| -V, --label name | Create the archive with the specified volume label name. |
| --version | Show the version number. |
| -w, --interactive, --confirmation | Ask for confirmation for every action. |
| -W, --verify | Verify the archive after creating it. |
| --exclude filename | Exclude the specified filename. You can use a shell pattern (see "Shell Patterns" in Chapter 4). |
| -X filename, --exclude-from filename | Exclude the files listed in the specified *filename*. |
| -Z, --compress, --uncompress | Use the compress program to compress or decompress the file. |
| -z, --gzip, --ungzip | Use the **gzip** program to compress or decompress the file. |
| --use-compress-program filename | Use the specified compression program. |
| --block-compress | Do not compress files routed to a tape device. |

## EXAMPLES

| This Command | Does the Following |
| --- | --- |
| `tar -cvf backup.tar /home/suzanne/documents` | Creates a new archive with the specified filename (backup.tar) and includes all the files in /home/suzanne/documents, including those in all of the associated subdirectories. |
| `tar -xvf backup.tar` | Extracts the files from the specified archive. By default, the extracted files will be placed in the directory from which they were archived. |
| `tar -cvf /dev/ftape /home/suzanne` | Creates a new archive on the specified tape device (/dev/ftape). Includes all the files in /home/suzanne, including those in all associated subdirectories. |
| `tar -xvzf kdbase.tgz` | Decompresses the specified compressed archive (kdbase.tgz) and extracts the files. |
| `tar -uvf backup.tar /home/suzanne` | Updates the specified archive (backup.tar) by adding only those files from /home/suzanne and all associated subdirectories that are not already present in the archive. |
| `find /home/suzanne -name '*.sdw' -print \| xargs tar -cvf backup.tar` | Finds all the StarWriter (*.sdw) files in /home/suzanne and adds them to a new archive named backup.tar. |

## unarj

**unarj [ option ] _archive_**

Decompresses or lists the contents of the specified ARJ archive. ARJ is an MS-DOS compression format. When used without an option, unarj lists the contents of the archive. It is not necessary to precede the options with a dash.

See also unzip.

### OPTIONS

| Use This Option | To Do This |
| :------------------ | :---------------- |
| e | Extract the files from the archive to the working directory |
| t | Test the archive’s integrity |
| x | Extract the files from the archive to their original location if the needed subdirectories exist |

## uncompress

uncompress [ option ] filename

Decompresses the compress (.Z) compressed file specified by filename. You can specify the filename by using a shell pattern (see the section "Shell Patterns" in Chapter 4) or a space-separated list. By default, the program prompts the user before overwriting existing files. You can suppress the confirmations by using the -f option. Use of this utility is discouraged because the underlying compression algorithm is patented. You can use gunzip to decompress .Z files.

### OPTIONS

| Use This Option | To Do This |
| :------------------ | :---------------- |
| -c | Write to the standard output |
| -f | Overwrite files without asking for confirmation |
| -V | Show version number |

## unzip

unzip [ option ] [ archive ] [ filename ]

Decompresses and extracts files from archives created by the Linux zip utility, PKZIP (MS-DOS), or WinZip (Microsoft Windows). For archive, specify the name of the zip archive you want to decompress.

The utility supplies the .zip suffix automatically. You can selectively extract files from the archive by specifying a filename, which can be the name of one of the files in the archive, a shell pattern (see the “Shell Patterns” section in Chapter 4), or a space-separated list of files. By default, unzip asks for confirmation before overwriting existing files. To suppress the confirmations, use the -o option. To compress files, use zip. To view information about files in a zip archive, see zipinfo.

TIP If you use a shell pattern, be sure to enclose the expression in double quotation marks so that the shell does not expand or modify the expression.

See also compress, bunzip2, gunzip.

### OPTIONS

| Use This Option | To Do This |
| :----- | :----- |
| -$ | Restore the volume label if the working medium is a removable disk. |
| -a | Automatically translate MS-DOS and Macintosh text files so that they conform to Linux line-feed conventions. |
| -b | Treat all files as if they were binary files. Omit automatic conversion of text files. |
| -c | Extract the files to the standard output and display the name of each file as it is extracted. |
| -C | Use case-insensitive filename matching. |
| -d directory | Extract the files to the specified directory instead of to the working directory. |
| -f | Freshen the files in the working directory by extracting only those files from the archive that are newer than the files in the working directory. |
| -j | Extract all the files in the archive to the working directory. Ignore path name information. |
| -l | Display the archive contents using the short format. |
| -L | Convert all filenames to lowercase. |
| -M | Display output on-screen with a text-paging utility. |
| -n | Skip the confirmation message for existing files. Never overwrites them. |
| -o | Overwrite existing files without prompting. |
| -p | Extract the files to the standard output without displaying the filenames. |
| -q | Hide program messages. |
| -s | Convert spaces in filenames to underscores. |
| -T | Set the timestamps on the archived files to that of the newest file in the archive. |
| -t | Test the integrity of the archived files by performing a checksum. |
| -u | Update an existing file in the working directory only if the archived file is newer than the one in the archive; also extract any files that are not present in the working directory. |
| -v | Display all program messages. |
| -X | Restore file ownership and permissions. |
| -x *filename* | Extract only the files specified by *filename*. You can use one filename, a space-separated list of filenames, or a shell pattern (see the “Shell Patterns” section in Chapter 4). Place this option at the end of the command. |
| -z | Display only the archive comment. Do not extract the files. |

### EXAMPLES

**This Command**

`unzip documents`

**Does the Following**

Decompresses all the files in the specified archive (*documents.zip*) and writes them to the working directory, or to the working directory and its associated subdirectories if the archive contains path name information.
