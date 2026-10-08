
# Environment Variables

See environ(5) for descriptions of the following environment variables that affect the execution of fgrep: LC_COLLATE, LC_TYPE, LC_MESSAGES, and NLPATH.

# Exit Status

- 0 Matches are found.
- 1 No matches are found.
- 2 Syntax errors or inaccessible files (even if matches are found).

# Attributes

See attributes(5) for descriptions of the following attributes:

# /usr/bin/fgrep

| Attribute Type | Attribute Value |
| --- | --- |
| Availability | SUNmcsu |

# /usr/xpg4/bin/fgrep

| Attribute Type | Attribute Value |
| --- | --- |
| Availability | SUNmxcu4 |
| CSI | Enabled |

# See Also

ed(1), egrep(1), grep(1), sed(1), sh(1), attributes(5), environ(5), largefile(5), XPG4(5).

# file — Determine File Type

# Synopsis

```
/usr/bin/file [-h] [-m mfile] [-f ffile] file
/usr/bin/file [-h] [-m mfile] -f ffile
/usr/bin/file -c [-m mfile]
```

# Description

The file command performs a series of tests on each file supplied by file and, optionally, on each file listed in ffile an attempt to classify it. If the file is not a regular file, its file type is identified. The file types directories, FIFO, block special, and character special are identified as such. If the file is a regular file and it is 0-length, it is identified as an empty file.

If file is a text file, it examines the first 512 bytes and tries to determine its programming language. If file is an executable a.out, file prints the version stamp, provided it is greater than 0. If file is a symbolic link, by default the link is followed and file tests the file to which the symbolic link refers.

# 356

# file

A magic number is a numeric string constant that indicates the file type. By default, file tries to use the localized magic file /usr/lib/locale/LC_MESSAGES/magic, if it exists, to identify files that have a magic number. If a localized magic file does not exist, file uses /etc/magic. See magic(4) for an explanation of the format of /etc/magic.

If file does not exist, cannot be read, or its file status could not be determined, it is not considered an error that affects the exit status. The output indicates that the file was processed, but that its type could not be determined.

# Options

- - c Check the magic file for format errors. For reasons of efficiency, validation is normally not carried out.
- - f ffile Examine the files listed in ffile.
- - h Do not follow symbolic links.
- - m mfile Use mfile as an alternative magic file, instead of /etc/magic.

# Operands

- ffile A file containing a list of the names of files to be examined.
- file A path name of a file to be tested.
- mfile An alternative magic file.

# Usage

See largefile(5) for the description of the behavior of file when encountering files greater or equal to 2 Gbytes (2**31 bytes).

# Examples

The following example displays the file types for all of the files in a directory.

```
castle file * directory
Art: Design.book: empty file
Mail: directory
Menu.status: empty file
ibliography: ascii text
checker.1: [nt]roff
```

The following example determines whether a file is a binary executable.
```
castle file "$1" | grep -Fq executable && printf "%s is executable.\n" "$1"
```

# Environment Variables

See environ(5) for descriptions of the following environment variables that affect the execution of file: LC_CTYPE, LC_MESSAGES, and NLSPATH.

# Exit Status

- 0 Successful completion.
- >0 An error occurred.

# Files

/etc/magic Magic number file.

# Attributes

See attributes(5) for descriptions of the following attributes:

| Attribute Type | Attribute Value |
| --- | --- |
| Availability CSI | SUNwcsu Enabled |

# See Also

ls(1), filehdr(4), magic(4), attributes(5), environ(5), largefile(5)

# Diagnostics

When you specify the -h option and file is a symbolic link, file prints the error message:
symbolic link to file

# filep — Front Ends to the mp Text to PDL Pretty Print Filter

# Synopsis

```
/bin/filep [options] filename...
```

# Description

See mailp(1).

# filesync — Synchronize Ordinary, Directory, or Special Files

# Synopsis

```
/usr/bin/filesync [-aehmnqvy] [-o src | dst] [-f src | dst] [-old | new]
-r directory...
/usr/bin/filesync [-aehmnqvy] -s source-dir -d dest-dir filename...
```

# Description

filesync synchronizes files between multiple computer systems, typically a server and a portable computer. filesync synchronizes ordinary, directory, or special files. Although intended for use on nomadic systems, filesync is useful for backup and file replication on permanently connected systems.

If files are synchronized between systems, files on each of the systems are identical. Changing a file on one or both systems can unsynchronize the files. To make the files identical again, the differences between the files must be reconciled.

There are two forms of filesync command. You invoke the first form of filesync without file arguments. This form of filesync reconciles differences between the files and systems specified in the $HOME/.packagerules file. $HOME/.packagerules is a rules list for filesync and cachepack contains a list of files to be kept synchronized. See filesync(4) and cachepack(1).

The second form of filesync copies specific files from a directory on the source system to a destination system. In addition, this form of filesync adds the file or files specified as arguments (filename) to $HOME/.packagerules. See -s and -d for information about specifying directories on source and destination systems.

Multiple filesync commands are cumulative (that is, the specified files are added to the already existing rules file list).

# Reconciling and Synchronizing Files

filesync synchronizes files between computer systems by performing the tasks:

- 1. filesync examines the directories and files specified in the packing rules file of both systems and determines whether they are identical.
- 2. filesync also maintains a baseline for all of the files being monitored.
- 3. If a file has changed and the destination file has not, the changes are propagated to the destination system.
- 4. If a file has changed and the source file has not, the changes are propagated to the source system.

# Resolving Conflicts

When files on both sides have changed, filesync tries to determine which version should win. If filesync cannot automatically determine which version should be, it prints a warning message and leaves the versions unreconciled.

In these cases, you must either resolve the differences or tell filesync how to choose using the -o and -f options.

# Packing Rules File

The packing rules file $HOME/.packrules contains a list of files to keep synchronized. The syntax of this file is described in packingrules(4).

If you invoke filesync with filename argument, the $HOME/.packrules is automatically created. By using filesync options, you can augment the packing rules.

Many users choose to create the rules file manually and edit it by hand. This allows access to more powerful options that are not available from the command line.such as By editing $HOME/.packrules, you can easily enter complex wild-card expressions.

# Baseline Files

$HOME/.filesync-base is the filesync baseline file, filesync uses the $HOME/.filesync-base to identify the differences between files during reconciliation and synchronization. You do not create or delete the baseline file. It is created automatically by filesync and records the last-known state of agreement between all of the files being maintained.

# Multiple filesync Commands

Over time, the files you want to keep synchronized can change. It is common, for instance, to keep files pertaining to only a few active projects on your notebook. If you continue to synchronize files associated with every project you have worked on, your notebook's disk will fill up with old files. In addition, each filesync command would waste a lot of time updating files you no longer care about.

If simply delete the files from your notebook, filesync wants to perform the corresponding deletes on the server, which is not what you want. Instead, you can tell filesync to stop synchronizing in one of the following ways:

- Edit $HOME/.packrules and delete the rules for the files you want to delete from your notebook.
- Delete $HOME/.packrules. Then, use the filesync command to specify the files that you want synchronized.

Either way works, and you can choose the one that seems easier to you. For minor changes, it is possibly easier to edit $HOME/.packrules. For major changes, it is possibly easier to start from scratch.
