
# rdist 1155

notify address...

Send mail to the indicated TCP/IP address of the form:
user@host
listing the files updated and any errors that may have occurred. If an address does not contain an @host suffix, use the name of the destination host to complete the address.

except filename...

Omit from updates the files named as arguments.

except_pat pattern...

Omit from updates the file names that match each regular expression pattern (see ed 1 for more information on regular expressions). Note that you must escape \ and $ characters in the distfile. You can also use shell variables with a pattern; however, shell file-name expansion is not supported.

special [filename] "command-line"

Specify a Bourne shell, sh(1), command line to execute on the remote host each name is updated. If you provide no filename argument, the command line is performed for every updated file, with the shell variable FILE set to the name of the file on the local host.

The quotation marks enable command-line to span input lines in the distfile, separate multiple shell commands with semicolons;

The default working directory for the shell executing each command line is the user's home directory on the remote host.

# IPv6

The rdist command is IPv6 enabled. See ip6(7P).

# Examples

The following sample distfile instructs rdist to maintain identical copies of a shared library, a shared library initialized data file, several includes, and a directory, on hosts named hermes and magus. On magus, commands are executed as superuser. rdist notifies mer@uid whenever a local file has changed relative to a timestamp file.

```
HOSTS = ( hermes root@magus )
FILES = ( /usr/local/lib/libcant.so.1.1
      /usr/local/lib/libcant.sa.1 /($HOME)/include/.*h)
      /usr/local/bin )
(${FILES}) -> (${HOSTS})
      install -R
      ${FILES} :: /usr/local/lib/timestamp
      notify mer@druid;
```

1156

read

# Files

```
~/.hosts      User's trusted hosts and users.
/etc/host.equiv  System trusted hosts and users.
/tmp/rdist*       Temporary file for update lists.
```

# Attributes

See attributes(5) for descriptions of the following attributes:

| Attribute Type | Attribute Value |
|---|---|
| Availability | SUNWrcmdc |

# See Also

csh(1), ed(1), sh(1), make(1S), stat(2), hosts.equiv(4), attributes(5),
ip6 (7P)

# Diagnostics

A complaint about mismatch of rdist version numbers can really stem from some problem with starting your shell, for example, you are in too many groups.

# Warnings

The superuser does not have the accustomed access privileges on NFS-mounted file systems. Using rdist to copy such a file system may fail or the copies may be owned by user nobody.

# Bugs

Source files must reside on or be mounted on the local host.
There is no easy way to have a special command executed once after all files in a directory have been updated.
Variable expansion works only for name lists; there should be a general macro facility.
dist aborts on files that have a negative modification time (before Jan. 1, 1970).
There should be a "force" option to enable replacement of nonempty directories by regular files or symbolic links. A means of updating file modes and owners of otherwise identical files is also needed.

# read — Read a Line from Standard Input

# Synopsis

```
/usr/bin/read [-r] var...
sh
read name...
```

# read

csh
set variable = $
ksh
read [-prsu[n]] [name?prompt] [name...]

# Description

**/usr/bin/read**
The read command reads a single line from standard input.
By default, unless you specify the -r option, backslash (\) acts as an escape character. If standard input is a terminal device and the invoking shell is interactive, read prompts for a continuation line in the following cases:

+   *When the shell reads an input ending with a backslash, -r option.*
- *When a here-document is not terminated after a newline character is entered.*

The line is split into fields as in the shell; the first field is assigned to the first var, the second field to the second variable var, and so forth. If you specify fewer operands than there are fields, the leftover fields and their separators are assigned to the last var. If you specify fewer fields than vars, the remaining vars are set to empty strings.
The setting of variables specified by the var operands affect the current execution environment. If read is called in a subshell or separate command execution environment, read does not affect the shell variables in the caller's environment.

```
(read foo)
nuhup read...
find -exec read... \
```

The standard input must be a text file.

**Bourne Shell**
One line is read from the standard input, and using the IFS internal field separator (normally space or Tab) to delimit word boundaries, the first word is assigned to the first name, the second word to the second name, and so forth, with leftover words assigned to the last name. Lines can be continued with \newline. You can quote characters other than newline by preceding them with a backslash. These backslashes are removed before words are assigned to names, and no interpretation is done on the character that follows the backlash. The return code is 0.

**C Shell**
One line is read from the standard input, and using the IFS internal field separator (normally space or Tab) to delimit word boundaries, the first word is assigned to the first name, the second word to the second name, and so forth, with leftover words assigned to the last name. Lines can be continued with \newline. You can quote characters other than newline by preceding them with a backslash. These backslashes are removed before words are assigned to names, and no interpretation is done on the character that follows the backlash. The return code is 0.

**Korn Shell**
One line is read from the standard input, and using the IFS internal field separator (normally space or Tab) to delimit word boundaries, the first word is assigned to the first name, the second word to the second name, and so forth, with leftover words assigned to the last name. Lines can be continued with \newline. You can quote characters other than newline by preceding them with a backslash. These backslashes are removed before words are assigned to names, and no interpretation is done on the character that follows the backlash. The return code is 0.

187

One line is read from the standard input, and using the IFS internal field separator (normally space or Tab) to delimit word boundaries, the first word is assigned to the first name, the second word to the second name, and so forth, with leftover words assigned to the last name. Lines can be continued with \newline. You can quote characters other than newline by preceding them with a backslash. These backslashes are removed before words are assigned to names, and no interpretation is done on the character that follows the backlash. The return code is 0.

# Options

+   p Provide the prompt string that an interactive shell writes to standard error.
-r Do not treat backslash in any way.
-s Save input as a command in the history file.
-u Read from file descriptor n.

# Operands

+var The name of an existing or nonexistent variable.

# Examples

The following example for /usr/bin/read prints a-each line.

```
while read -rx xx
do
    printf "%s\n" "$yy"
done < input_file
```

0 End-of-file was detected or an error occurred.

# Attributes

See attributes(5) for descriptions of the following attributes.

| Attribute Type | Attribute Value |
|---|---|
| Availability | SUNWcsu |

# See Also

csh(1), ksh(1), line(1), set(1), sh(1), attributes(5), environ(5)

# readonly — Shell-In Function to Protect the Value of the Given Variable from Reassignment

# Synopsis

```
sh
readonly [name...]
ksh
**
readonly [name=value]
```

# Description

Bourne Shell
The names you specify are marked readonly, and the values of the names cannot be changed by subsequent assignment. If you specify no arguments, a list of all readonly names is printed.

Korn Shell
The given names are marked readonly and cannot be changed by subsequent assignment.
the readonly command, ksh(1) commands that are preceded by one or two asterisks (*) are treated specially in the following ways.

- Variable assignment lists preceding the command remain in effect until the command completes.
- I/O redirections are processed after variable assignment.
- Errors abort a script that contains them.
- Words following a command preceded by ** that are in the format of a variable assignment are expanded with the same rules as a variable assignment. This means that tilde substitution is performed after the equal sign and word splitting and file-name generation are not performed.

# Attributes

See attributes(5) for descriptions of the following attributes.

| Attribute Type | Attribute Value |
|---|---|
| Availability | SUNWcsu |

# See Also

ksh(1), sh(1), typeset(1), attributes(5)
