
## COMMANDS (CONT.)

| Use This Command | To Do This |
|---|---|
| `--lsign-key` *name* | Sign a public key with your signature but mark it as unexportable. |
| `-s`, `--sign` | Create a digital signature. |
| `--send-keys` \{ *user ID* \} | Send all public keys, or just those of the specified user ID, to a keyserver. Specify the keyserver with `--keyserver`. |
| `--sign-key` *user ID* | Sign a public key with your secret key. |
| `--verify` \[ *filename* \] | Verify the digital signature in the specified filename. |
| `--version` | Show the version number. |
| `--warranty` | Display warranty information. |

## EXAMPLES

| This Command | Does the Following |
|---|---|
| `gpg --gen-key` | Generates a new key pair. |
| `gpg --clearsign` *mysig* | Creates a cleartext signature. |
| `gpg -e` *autobiography.doc* | Encrypts the specified file. You will be prompted for a destination user ID. |
| `gpg --list-keys` | Shows all the public keys on the current key ring. |
| `gpg --decrypt` *autobiography.doc.gpg* | Decrypts the specified file. You will be prompted for the passphrase. |

## gunzip

`gunzip [ option ] filename`

Decompresses the specified **filename**. For *filename*, you can use a shell pattern (see the section "Shell Patterns" in Chapter 4) or a space-separated list of files. This utility can decompress files created with the following utilities: **compress (.Z), gzip (.gz, .t2g)**, and **zip (.zip)**. By default, **gzip** does not overwrite existing output files. Use the **--force** option to override this setting.

See also **zcat** (Chapter 8).

## OPTIONS

| Use This Option | To Do This |
|---|---|
| **-c, --stdout, --tostdart** | Route output to the standard output |
| **-f, --force** | Force overwrite of output files |
| **-h, --help** | Display available options |
| **-L, --license,** | Display the software version and license terms and conditions |
| **-l, --list** | For each compressed file, list the compressed size, uncompressed size, compression ratio, and name of the uncompressed file |
| **-n, --noname** | Skip saving the original file's name and timestamp |
| **-N, --name** | Save the original file's name and timestamp |
| **-q, --quiet** | Suppress most program messages, except those concerning input and output errors |
| **-r, --recursive** | Compress all the specified directories and all of their associated subdirectories |
| **-t, --test** | Test the files to see whether they are valid and decompressable |
| **-v, --verbose** | Display messages as each file is processed |
| **-V, --version** | Show the version number |

## gzexe

`gzexe [ filename ]`

Compresses the executable file specified by *filename* so that it automatically decompresses and executes when you run it. Although compressing an executable in this way saves disk storage space, the executable takes longer to start. The program automatically backs up the original file with the `~` suffix. You can remove this backup file when you are sure that the compressed executable runs correctly.

## OPTION

| Use This Option | To Do This |
|---|---|
| `-d` | Decompress the executable file |

## EXAMPLE

| This Command | Does the Following |
|---|---|
| `gzexe /usr/local/Office51/bin/soffice` | Compresses the specified executable so that it occupies less disk space. |

## gzip

`gzip [ option ] *filename*`

Compresses the specified *filename* using a patent-free compression algorithm (LZ77). For *filename*, specify the name of the file or files to be archived. You can use a shell pattern (see the section “Shell Patterns” in Chapter 4), a space-separated list of files, or a directory name. With the `-r` option, you can quickly compress all the files in a directory tree. By default, gzip does not overwrite existing output files (use the `--force` option to override this setting), but the program replaces input files with compressed files that have the `.gz` extension. To decompress the files, use gunzip.

See also compress, bzip2.

## OPTIONS

| Use This Option | To Do This |
|---|---|
| **-1, -2, -3, -4, -5, -6, -7, -8, -9** | Specific compression performance on a continuum from 1 to 9, with 1 giving the best *speed* but poorest compression ratio (equivalent to `--fast`) and 9 giving the slowest speed but best compression ratio (equivalent to `--best`). The default is **-6**. |
| **--best** | Compress for the smallest possible file size at the cost of execution speed. |
| **-c, --stdout, --to-stdout** | Route output to the standard output. |
| **-d, --decompress, --uncompress** | Force gzip to decompress files. This is the same as running gunzip. |
| **-f, --force** | Force the overwrite of output files. |
| **-fast** | Compress quickly at the cost of a larger compressed file size. |
| **--help** | Display available options. |
| **-L, --license** | Display the license terms and conditions. |
| **-n, --no-name** | Skip reporting the original file’s name and timestamp. |
| **-N, --name** | Save the original filename and timestamp. This is the default. |
| **-q, --quiet** | Suppress most program messages, except those concerning input and output errors. |
| **-r, --recursive** | Compress the specified directory and all of its associated subdirectories. |
| **-S *suffix*, --suffix *suffix*** | Use the specified suffix instead of the program default (.gz). |
| **-v, --verbose** | Display messages as each file is processed. |
| **-V, --version** | Show the version number. |

## EXAMPLES

| This Command | Does the Following |
|---|---|
| `gzip massivefile.txt` | Compresses the specified file (*massivefile.txt*). |
| `gzip --best massivefile.txt` | Compresses the specified file (*massivefile.txt*) using the compression method that yields the maximum reduction in size. |
| `gzip -r /home/suzanne/documents` | Compress all the files in the specified directory and all of its associated subdirectories. |

## hexbin

`hexbin [ option ] filename`

Extracts files from a Macintosh binhex (*.bin,*.hqx*) archive. By default, the program extracts files from the specified *filename* and writes the output to the working directory. This utility is part of the MacUtils package which is available on the following ftp site: *metalab.unc.edu/pub/linux/utils/compress*.

See also *macunpack, hexbin*.

## OPTIONS

| Use This Option | To Do This |
|---|---|
| `–3` | Write files in fork format (info, data, and rsrc). |
| `–a` | Save in AppleShare format in a valid AppleShare folder. |
| `–c` | Skip checking to make sure all lines are of equal length. |
| `–d` | Write data forks only. |
| `–f` | Write files in fork format but skip empty data and resource forks. |
| `–H` | Show available options. |

## OPTIONS (CONT.)

| Use This Option | To Do This |
|---|---|
| `-i` | Provide information only. |
| `-l` | List information about the files being extracted. |
| `-n` *filename* | Use the specified filename. |
| `-q` | Ask for confirmation before extracting files. |
| `-r` | Write resource forks only. |
| `-s` | Write extracted files to standard output in MacBinary format. |
| `-u` | Write data forks only but use Linux line-feed conventions and name the files with the .text suffix. |
| `-U` | Write data forks only but use Linux line-feed conventions. No suffix is added. |
| `-v` | Show all available messages. |
| `-V` | Show the version number. |

## macunpack

`macunpack [ option ] filename`

Extracts files from a Macintosh MacBinary archive (generally saved with the .bin suffix). By default, the program extracts the files to the working directory and creates subdirectories, if needed, for files saved with path information. This utility is part of the Macutils package, which is available on the following ftp site: *metalab.unc.edu/pub/linux/utils/compress*.

See also hexbin.

## OPTIONS

| Use This Option | To Do This |
|---|---|
| `-3` | Write files in fork format (info, data, and rsrc). |
| `-a` | Save in AppleShare format in a valid AppleShare folder. |
| `-d` | Write data forks only. |
