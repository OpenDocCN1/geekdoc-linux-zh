
# 364

# Files

$HOME/.packingrules
List of files to be kept synchronized.

$HOME/.filesync-base
Baseline summary file.

# Attributes
See attributes(5) for descriptions of the following attributes:

| Attribute Type | Attribute Value |
|---|---|
| Availability | SUNWcmd |

# See Also
cachefpack(1M), packingrules(4), attributes(5)

# filofaxp — Front Ends to the mp Text to PDL Pretty Print Filter

# Synopsis
/bin/filofaxp [options] filename...

# Description
See mailp(1).

# find — Find Files

# Synopsis
/usr/bin/find path... expression
/usr/xpg/find path... expression

# Description
You can use the find command to search through any part of the file system, looking for files with a particular name. find recursively descends the directory hierarchy for each path, seeking files that match expression.
find descends to arbitrary depths in a file hierarchy and does not fail because of path-length limitations (unless a path operand specified by the application exceeds PATH_MAX requirements).

# find

# Operands

A path name of a starting point in the directory hierarchy. Interpret the first argument that starts with a -, or is a ! or (, and all subsequent arguments as an expression made of the following primaries and operators.

+ - path
- expression In the descriptions, wherever use n as a primary argument, interpret it as a decimal integer optionally preceded by a plus (+) or minus (-) sign, as follows:

  + +n More than n.
  - -n Exactly n.
  - -n Less than n.

# Expressions

+ -atime n if the file was accessed n days ago. The access time of directories in path is changed by find itself.

+ -cpio device Always true; write the current file on device in cpio format (5120-byte records).
-ctime n if any aspect of the file's inode was changed n days ago.
-depth Always true; descend the directory hierarchy so that all entries in a directory are acted on before the directory itself. This option can be useful when find is used with cpio(1) to transfer files that are contained in directories without write permission.

> -exec command if the executed command returns a 0 value as exit status. You must punctuate the end of command with an escaped semicolon. A command argument (\}) is replaced by the current path name.
If the last argument to -exec is {} and you specify instead of the semicolon \;, the command is invoked fewer times, with {} replaced by groups of path names. In the Solaris 9 release.

+ -follow Always true; follow symbolic links. When following symbolic links, keeps track of the directories visited so that it can detect infinite loops. For such a loop would occur if a symbolic link pointed to an ancestor. Do not use this expression with the -type 1 expression.

+ -fstype type if the file system to which the file belongs is of type type.

+ -group gname if the file belongs to the group name. If it is numeric and does not appear in the /etc/group file or in the NIS or NIS+ tables, it is taken as a group ID.

+ -inum n true if the file has number n
-links n true if the file has links.

-local true if the file-system type is not a remote file-system type as defined in the /etc/dfs/fstypes file. uses nfs as the default remote file-system type if the /etc/dfs/fstypes file is not present.

Note that -local descends the hierarchy of nonlocal directories. "Examples" on page 369 for an example of how to search for local files without descending.

-ls Always true; print current path name together with its associated statistics:

  * Inode number.
* Size in kilobytes (1024 bytes).
* Protection mode.
* Number of hard links.
* User.
* Group.
* Size in bytes.
* Modification time.

If the file is a special file, the size field contains the major and minor device numbers. If the file is a symbolic link, the path name of the linked-to file is printed by ->. The format is identical to that of ls -gilds (see ls(1)). Formatting is done internally, without executing the ls command.

-mount Always true; restrict the search to the file system containing the directory specified. Do not list mount points to other file systems.

-mtime n true if the contents of the file was modified n days ago.

-name pattern true if pattern matches the current file name. You can use normal shell-file name generation characters (see sh(1)). Use a backslash (\) as an escape character within the pattern. Escape or quote the pattern when you invoke find from the shell.

Unless you explicitly specify the character at the beginning of a pattern, a current file name beginning does not match pattern with the /usr/bin/find command. The /usr/xpg/bin/find command does not make this distinction. Wild-card file-name generation characters can match file names beginning with a dot (.). New in the Solaris 9 release.

-ncpio device Always true; write the current file on device in cpio -c format (5120-byte records).

-size anum[] true if the file is anum blocks long (512 bytes per block). If you follow anum with a c, the size is in bytes.

# 366 find

# find

-type c true if the type of the file is c, where c is b (block special file), c (character special file), d (directory), l (symbolic link), p (fifo named) pipe, s (socket), or f (plain file).

-user uname true if the file belongs to the user name. If username is numeric and does not appear as a login name in the /etc/passwd file or in the NIS or NIS+ classes, take it as a user ID.

New!

-xattr true if the file has extended attributes. New in the Solaris 9 release.

-xdev Same as the -mount primary.

New!

> Note — When using find to determine files modified within a range of time, specify the -atime, -ctime, or -mtime option before the -print option; otherwise, find gives all files.

New!

Some paths that may be under the Solaris root system are actually mount points for virtual file systems such as nfs or namesfs. When comparing against a UFS file system, they are not selected if you specify -mount or -xdev in the find expression.

The following options are obsolete and will not be supported in future releases.

-cpio device Always true; write the current file on device in cpio format (5120-byte records).

-ncpio device Always true; write the current file on device in cpio -c format (5120-byte records).

# Complex Expressions

You can combine the primaries by using the operators listed below, in order of decreasing precedence.

(expression) true if the parenthesized expression is true (parentheses special to the shell and must be escaped).

! expression The negation of a primary (! is the unary operator).

expression [-a] expression Concatenation of primaries (the and operation is implied by the juxtaposition of two primaries).

expression -o expression Alternation of primaries (-o is the or operator).

# 398 find

> > Note — When you use find in conjunction with cpio, if you use the -L option with cpio, then you must use the -follow expression with find, and vice versa. Otherwise, you get undesirable results.

If no expression is printed, -print is used as the expression. Otherwise, if the expression does not contain any of the primaries -exec, -ok, or -print, the given expression is effectively replaced by:
(given-expression) -print

-user,-group, and -newer primaries each evaluate their respective arguments once. Invoking the command specified by -exec or -ok does not affect subsequent primaries on the same file.

# Usage

See large(5) for the description of the behavior of find when encountering files greater than or equal to 2 Gbytes (*31 bytes).

# Examples

The following commands are equivalent. Both write out the entire directory hierarchy from the current directory.

```
castle% find
castle% find -print
castle# find / -name core -print
/export/home/winsor/core
/files/winsor/bookgames/src/xblackjack/core
castle#
```

The following example searches from the root directory (/) and lists all core files on the system.

The following example searches the current directory and silently removes all core files.

```
castle% pwd
/export/home/winsor
castle% ls core
castle% find -name core -exec rm {} \
castle% ls core
core: No such file or directory
castle%
```

If you want to see a list of the files that are removed, add the -print option to the command line as shown in the following example.

```
castle% find -name core -exec rm {} \ -print
```

The following example recursively prints all file names whose permission mode matches read, write, and execute access for user, and read and execute access for group and other.
