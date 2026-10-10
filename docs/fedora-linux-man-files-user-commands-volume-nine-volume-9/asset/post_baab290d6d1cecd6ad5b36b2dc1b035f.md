
## BUGS

If you find a bug, please report it at

## AUTHORS

- Jacob Perkins <>
- Jose Carlos Garcia Sogo <>
- Jean Schurger <>
- Stef Walter <>
- Adam Schreiber <>

## SECON

### NAME

secon - See an SELinux context, from a file, program or user input.

### SYNOPSIS

**secon** [-h | -V | -u | -r | -s | -c | -m | -P | -C | -R | -f | -L | -p] [CONTEXT] [--file FILE] [--link FILE] [--pid PID]

### DESCRIPTION

See a part of a context. The context is taken from a file, pid, user input or the context in which **secon** is originally executed.

- -V, —version
  shows the current version of secon
- -h, —help
  shows the usage information for secon
- -P, —prompt
  outputs data in a format suitable for a prompt
- -C, —color
  outputs data with the associated ANSI color codes (requires -P)
- -u, —user
  show the user of the security context
- -r, —role
  show the role of the security context
- -t, —type
  show the type of the security context
- -s, —sensitivity
  show the sensitivity level of the security context
- -c, —clearance
  show the clearance level of the security context
- -m, -s-range
  show the sensitivity level and clearance, as a range, of the security context
- -R, —raw
  outputs the sensitivity level and clearance in an untranslated format.
- -f, —file
  gets the context from the specified file FILE
- -L, —link
  gets the context from the specified file FILE (doesn't follow symlinks)
- -p, —pid
  gets the context from the specified process PID
- —pid-exec
  gets the exec context from the specified process PID
- —pid-fs
  gets the fscreate context from the specified process PID
- —current, —self
  gets the context from the current process
- —current-exec, —self-exec
  gets the exec context from the current process
- —current-fs, —self-fs
  gets the fscreate context from the current process
- —parent
  gets the context from the parent of the current process
- —parent-exec
  gets the exec context from the parent of the current process
- —parent-fs
  gets the fscreate context from the parent of the current process

Additional argument CONTEXT may be provided and will be used if no options have been specified to make secon get its context from another source. If that argument is - then the context will be read from stdin. If there is no argument, secon will try reading a context from stdin, if that is not a tty, otherwise secon will act as though —self had been passed.

If none of —user, —role, —type, —level or —s-range is passed. Then all of them will be output.

### SEE ALSO

- **chcon** (1)

### AUTHORS

Jas Antill ()

## SECRET-TOOL

### NAME

secret-tool - Store and retrieve passwords

### SYNOPSIS

secret-tool store —label='Label' {attribute} {value} ...
secret-tool lookup {attribute} {value} ...
secret-tool clear {attribute} {value} ...
secret-tool search [--all] {attribute} {value} ...

### DESCRIPTION

**secret-tool** is a command line tool that can be used to store and retrieve passwords.

Each password is stored in an item. Items are uniquely identified by a set of attribute keys and values. When storing a password you must specify unique pairs of attributes names and values, and when looking up a password you provide the same attribute name and value pairs.

### STORE

To store a password run **secret-tool** with the store argument. You must also specify a label for the password with the —label argument. This label will be displayed in the password manager.

Make sure to pass a unique set of attributes names and values when storing a password. If the attributes match an already existing item, it will be updated instead of creating a new item. If invoked from a terminal or tty, then the password to store will be prompted for and only one line will be accepted.

A password to store can also be piped in via stdin. The password will be the contents of stdin until EOF. If you provide a newline via stdin it will be stored as part of the password.

### LOOKUP

To lookup a password run `secret-tool` with the lookup argument. Specify the same attribute names and value pairs that you passed when storing the password.

If multiple items match the attribute provided, then the first password that is already unlocked will be returned. If necessary an item will be unlocked.

When printing the password to a terminal or tty, an extra newline will be added after the password.

### CLEAR

To remove a password run **secret-tool** with the clear argument. Specify the same attribute name and value pairs that you passed when storing the password. All unlocked items that match the attributes will be removed.

### SEARCH

This command searches for and prints details on matching items in secret service. Specify the same attribute and value pairs that you passed in when storing the password. You can use the following options:

- —all
  Return all matching results, rather than just the one of the matches. Without this option, the first unlocked match returned from the service will be printed.
- —unlock
  Unlock items that are locked and then print out their details. Without this option, locked items are skipped.

### EXIT STATUS

On success 0 is returned, a non-zero failure code otherwise.

### EXAMPLES

#### Example 1. Storing, retrieving, and clearing a password

```
$ secret-tool store --label='My password' key1 value1 key2 value2
Password: My password
```

```
$ secret-tool lookup key1 value1 key2 value2
My password
```

```
$ secret-tool clear key1 value1 key2 value2
```

## SED

### NAME

sed - stream editor for filtering and transforming text

### SYNOPSIS

```
sed [OPTION]... {script-only-if-no-other-script} [input-file]...
```

### DESCRIPTION

Sed is a stream editor. A stream editor is used to perform basic text transformations on an input stream (a file or input from a pipeline). While in some ways similar to an editor which permits scripted edits (such as ed), sed works by making only one pass over the input(s), and is consequently more efficient. But it is sed’s ability to filter text in a pipeline which particularly distinguishes it from other types of editors.

- -n, --quiet, --silent
  suppress automatic printing of pattern space
- -e script, --expression=script
  add the script to the commands to be executed
- -f script-file, --file=script-file
  add the contents of script-file to the commands to be executed
- --follow-symlinks
  follow symlinks when processing in place
- -i[SUFFIX], --in-place[=SUFFIX]
  edit files in place (makes backup if SUFFIX supplied)
- -c, --copy
  use copy instead of rename when shuffling files in -i mode
- -b, --binary
  does nothing; for compatibility with WIN32/CYGWIN/MSDOS/EMX (open files in binary mode (CR+LFs are not treated specially))
- -l N, --line-length=N
  specify the desired line-wrap length for the \l command
- --posix
  disable all GNU extensions.
- -r, --regexp-extended
  use extended regular expressions in the script.
- -s, --separate
  consider files as separate rather than as a single continuous long stream.
- -u, --unbuffered
  load minimal amounts of data from the input files and flush the output buffers more often
- -z, --null-data
  separate lines by NUL characters
- --help
  display this help and exit
- --version
  output version information and exit

If no -e, --expression, -f, or --file option is given, then the first non-option argument is taken as the sed script to interpret. All remaining arguments are names of input files; if no input files are specified, then the standard input is read.
