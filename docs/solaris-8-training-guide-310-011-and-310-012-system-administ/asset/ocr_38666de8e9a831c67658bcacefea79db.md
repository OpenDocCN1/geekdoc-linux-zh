# dd

The main advantage of the dd command is that it quickly converts and copies files with different data formats, such as differences in block size or record length.

The most common use of dd is to transfer a complete file system or partition from your hard disk to a tape. You can also use it to copy files from one hard disk to another. When you’re copying data, the dd command makes an image copy (an exact byte-for-byte copy) of any medium, which can be either tape or disk. The command arguments are described in Table 11.4. The syntax for the dd command is as follows:

```
dd if=<input-file> of=<output-file> <option=value>
```

# TABLE 11.4

# dd COMMAND ARGUMENTS

| Argument | Description |
|---|---|
| if | Used to designate an input file. The input file can be a filename or a device name, such as /dev/rmt/0. If no input file is specified, input for dd is taken from the UNIX standard input. |
| of | Used to designate an output file. The output file can be a filename or a device name, such as /dev/rmt/0. If no output file is specified, output from dd is sent to the UNIX standard output. |

Several other options can follow on the command line to specify buffer sizes, block sizes, and data conversions. See the Solaris online manual pages for a list of these options.

# dd Examples

The next few examples illustrate the use of the dd command to copy data. The first example shows how the dd command is used to duplicate tapes. This procedure requires two tape drives—a source tape and a destination tape:

```
dd if=/dev/rmt/0 of=/dev/rmt/1
```