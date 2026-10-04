# Table 11-5 Command Options for pax

| Option | Description |
|---|---|
| -r | Reads an archive file from standard input and extracts the specified files. If any intermediate directories are needed for extracting an archive member, these directories are created. |
| -w | Writes files to the standard output in the specified archive format. When no file operands are specified, standard input is read as a list of pathnames—one per line, without any leading or trailing blanks. |
| -a | Appends files to the end of an archive that was previously written. |
| -b | Blocksize. The blocksize must be a multiple of 512 bytes, with a maximum of 32,256 bytes. A blocksize can end with k or b to specify multiplication by 1,024 (1K) or 512, respectively. |
| -c | Matches all file or archive members except those specified by the pattern and file operands. |
| -f <archive> | Specifies archive as the pathname of the input or output archive. A single archive may span multiple files and different archive devices. When required, pax prompts for the pathname of the file or device of the next volume in the archive. |
| -n | Selects the first archive member that matches each pattern operand. No more than one archive member is matched for each pattern. |
| -p <string> | Specifies one or more file characteristic options (privileges). The string option-argument is a string specifying file characteristics to be retained or discarded on extraction. The string consists of the specification characters a, e, m, o, and p. Multiple characteristics can be concatenated within the same string and multiple -p options can be specified. The meanings of the specification characters are as follows:

 a—Do not preserve file access times.
 e—Preserve everything: user ID, group ID, file mode bits, file access times, and file modification times.
 m—Do not preserve file modification times.
 o—Preserve the user ID and group ID.
 p—Preserve the file mode bits. |
| -v | Verbose mode. |
| -x <format> | Specifies the output archive format, with the default format being ustar. pax currently supports cpio, tar, bcpio, ustar, sv4crc, and sv4cpio. |

When using pax, you can also specify file operands along with options from Table 11-5. The operand specifies a destination directory or file pathname. If you specify a directory operand but the directory operand does not exist, is not writable by the user, or is not of type directory, pax exits with a non-zero exit status.

The file operand specifies the pathname of a file to be copied or archived. When a file operand does not select at least one archive member, pax writes these file operand pathnames in a diagnostic message to standard error and then exits with a non-zero exit status.