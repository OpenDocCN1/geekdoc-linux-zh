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