You must use Berkeley-compatible device names with the tcopy command, as shown in the following example:

```
mopoke@ tcopy /dev/rmt /dev/rmt/2b
```

# Attributes

See attributes(5) for descriptions of attributes:

| Attribute Type | Attribute Value |
|---|---|
| Availability | SUNmesu |

# See Also

mt(1), ioctl(2), attributes(5)

# tee Replicate the Standard Output

# Synopsis

```
/usr/bin/tee [-ai] [file...]
```

# Description

The tee command is analogous to a tee joint in plumbing that splits an incoming stream of water. tee splits standard input into two or more output streams, sending one to standard output and the others to files you specify on the command line.

You can use the tee command to monitor a command to make sure it is doing what you want to save or as an intermediate step in a pipeline sequence, tee does not buffer its output. The options determine whether the specified files are overwritten or appended to.

# Options

+   -a Append the output to the files instead of overwriting.
-i Ignore interrupts.

# Operands

+   - A path name of an output file. You can process at least 13 operands.

# Examples

The following example uses the file command to display information about files in the current directory and also saves a copy of the information in a file named filetypes.

```
castle% * | tee filetypes
085DOC.zip: data
Appletver.rs: rasterfile, 511 x 18 x 8 standard format image
Mail: directory
ibliography: ascii text
ELF 32-bit MSB core file SPARC Version 1, from 'srchtrt'
core: tee *
```