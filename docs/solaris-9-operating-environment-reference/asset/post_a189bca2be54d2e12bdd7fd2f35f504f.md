
# 158

## command

## -V

Write a string to standard output that indicates the name given in the `command-name` operand is interpreted by the shell in the current shell execution environment. Although the format of this string is unspecified, it indicates in which of the following categories `command-name` falls and includes the information stated below.

+ - Identify commands, regular built-in commands, and any implementation-provided functions that are found, using the PATH variable, and include the absolute path name in the string.
+ - Identify other shell functions.
+ - Identify aliases and include their definitions in the string.
+ - Identify special built-in commands.
+ - Identify regular built-in commands not associated with a PATH search.
+ - Identify shell reserved commands.

## Operands

+ argument: One of the strings treated as an argument to `command-name`.
+ command-name: The name of a command or a special built-in command.

## Examples

The following example makes a version of cd that always prints out the new working directory exactly once.

```
cd() {
command cd "$@" /dev/null
pwd
}
```

The following example starts a secure shell script in which the script avoids being fooled by its parent.

```
IFS='
# The preceding value should be <space><tab><newline>.
# Set IFS to its default value.
\unalias
# Set all possible aliases.
# Note that aliases is escaped to prevent an alias
# being used for aliases.
unset -f command
# Ensure command is not a user function.
PATH="$(command -p CS_PATH):$PATH"
# Put on a reliable PATH prefix.
#...
```

At this point, given correct permissions on the directories called by PATH, the script can ensure any command it calls is the intended one. The script is very cautious because it assumes implementation extensions may be present that would allow user functions to exist when it is invoked; this capability is not specified by this document, but it is not prohibited as an extension. For example, the ENV variable precedes the invocation of the script with a user startup script. Such a script could define functions to spoof the application.

## Environment Variables

environ(5) for descriptions of the following environment variables that affect the execution of command: LC_CTYPE, LC_MESSAGES, and NLSPATH.

PATH Determine the search path, used during the command search, except as described under the -p option.

## Exit Status

When you use the -v or -V options, the following exit values are returned:

+ 0 Successful completion.
+ >0 The command-name could not be found, or an error occurred.

Otherwise, the following exit values are returned:

+ 126 The command specified by command-name was found but could not be invoked.
+ 126 An error occurred in the command command, or the command specified by command-name could not be found.

Otherwise, the exit status of command is that of the simple command specified by the arguments to command.

## Attributes

attributes(5) for descriptions of the following attributes

| Attribute Type | Attribute Value |
|---|---|
| Availability | SUNWcsu |

## See Also

sh(1), type(1), attributes(5)

# compress, uncompress, zcat — Compress, Uncompress Files or Display Expanded Files

## Synopsis

```
/usr/bin/compress [-fv] [-b bits] [file...]
/usr/bin/compress [-cfv] [-b bits] [file]
/usr/bin/uncompress [-cfv] [file...]
/usr/bin/zcat *
```

## compress, uncompress, zcat

## Description

### compress

The compress command tries to reduce the size of the named files by using adaptive Ziv coding. Except when the output is to the standard output, each file is replaced by one with the extension .z, while keeping the same ownership modes, change times, and modification times.

If appending a .z to the file name would make the name exceed 14 bytes, the command fails. If no files are specified, the standard input is compressed to the standard output.

The amount of compression depends on the size of the input, the number of bits per code, and the distribution of common substrings. Typically, such source code or English is reduced by 50-60 percent. Compression is generally much better than that achieved by Huffman coding (as used in pack(-)) and takes less time to compute. The bits parameter specified during compression is encoded within the compressed file, along with a magic number to ensure that neither decompression of random data nor recompression of compressed data is followed afterwards.

> Note — Although compressed files are compatible between machines with large memory, use -b 12 for file transfer to architectures with a small process data state (64 kilobytes or less).

compress should be more flexible about the existence of the .z suffix.

### uncompress

The uncompress command restores files to their original state after they have been compressed by the compress command. If you specify no files, the standard input is uncompressed to the standard output.

This command supports the uncompressing of any files produced by compress. Files produced by compress on other systems, uncompress supports 9 to 16-bit compression (see -b).

### zcat

The zcat command writes to standard output the uncompressed form of files that have been compressed with compress. It is the equivalent of uncompress -c. Input files are not affected.

## Options

+ -b bits The upper limit (in bits) for code. Bits must be between 9 and 16.
+ -c Write to standard output.
+ -f Force compression or decompression, even if file would increase in size.
+ -v Write percentage of the input saved by compression. (Relevant only for compress)

## Operands

+ file: A path name of a file to be compressed. If no file is specified, standard input is used.

## Examples

The following example compresses and uncompresses a file named test. As you can see, uncompressed is about 50 percent smaller.

```
$ compress -v test
$ uncompress -v test.z
$ zcat test.z
```
