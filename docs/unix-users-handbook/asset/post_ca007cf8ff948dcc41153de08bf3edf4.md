
that is received. No output is produced if there are no responses.
If an optional count is given, only the specified number of requests is sent. Round-trip times and packet loss statistics are computed. When all responses have been received or the command times out (if the count option is specified), or if the command is terminated with a SIGINT, a brief summary is displayed.

This command is intended for use in testing, managing and measuring network performance. It should be used primarily to isolate network failures. Because of the load it could impose on the network, it is considered discourteous to use ping unnecessarily during normal operations or from automated scripts.

## AUTHOR

ping was developed in the Public Domain.

## FILES

/etc/hosts

## SEE ALSO

gethostbyname(3N), inet(3N).

# rcp

**rcp** - Copy files and directories from one system to another.

![](img/75f39fc91296b889c0653851accdfd46_564_0.png)

rcp(1)

## NAME

rcp - remote file copy

## SYNOPSIS

- Copy Single File:
  `rcp [-p] source_file dest_file`
- Copy Multiple Files:
  `rcp [-p] source_file1 [source_file2]... dest_dir`
- Copy One or More Directory Subtrees:
  `rcp [-p] -r source_dir1 [source_dir2]... dest_dir`
- Copy Files and Directory Subtrees:
  `rcp [-p] -r file_or_dir1 [file_or_dir2]... dest_dir`

## DESCRIPTION

The rcp command copies files, directory subtrees, or a combination of files and directory subtrees from one or more systems to another. In many respects, it is similar to the cp command (see cp(1)).

To use rcp, you must have read access to files being copied, and read and search (execute) permission on all directories in the directory path.

### Options and Arguments

rcp recognizes the following options and arguments:

- **source_file**: The name of an existing file or directory on a local or remote machine that you want copied to the specified destination. Source file and directory names are constructed as follows:
  `user_name@hostname:pathname/filename`
  or
  `user_name@hostname:pathname/dirname`
  
  Component parts of file and directory names are described below. If multiple existing files and/or directory subtrees are specified (*source_file1*, *source_file2*, ..., etc.), the destination must be a directory. Shell file name expansion is allowed on both local and remote systems. Multiple files and directory subtrees can be copied from one or more systems to a single destination directory with a single command.

- **dest_file**: The name of the destination file. If host name and path name are not specified, the existing file is copied into a file named *dest_file* in the current directory on the local system. If *dest_file* already exists and is writable, the existing file is overwritten. Destination file names are constructed the same way as source files except that file name expansion characters cannot be used.

- **dest_dir**: The name of the destination directory. If host name and path name are not specified, the existing file is copied into a directory named *dest_dir* in the current directory on the local system. If *dest_dir* already exists in the specified directory path (or current directory if not specified), a new directory named *dest_dir* is created underneath the existing directory named *dest_dir*. Destination directory names are constructed the same way as source directory tree names except that file name expansion characters cannot be used.

- **file_or_dir**: If a combination of files and directories are specified for copying (either explicitly or by file name expansion), only files are copied unless the *-r* option is specified. If the *-r* option is present, all files and directory subtrees whose names match the specified *file_or_dir* name are copied.

- **-P**: Preserve (duplicate) modification times and modes (permissions) of source files, ignoring the current setting of the *umask* file creation mode mask. If this option is specified, *rcp* preserves the sticky bit only if the target user is superuser.

If the *-p* option is not specified, *rcp* preserves the mode and owner of *dest_file* if it already exists; otherwise *rcp* uses the mode of the source file modified by the *umask* on the destination host. Modification and access times of the destination file are set to the time when the copy was made.

- **-R**: Recursively copy directory subtrees rooted at the source directory name. If any directory subtrees are to be copied, *rcp* recursively copies each subtree rooted at the specified source directory name to directory *dest_dir*. If *source_dir* is being copied to an existing directory of the same name, *rcp* creates a new directory *source_dir* within *dest_dir* and copies the subtree rooted at *source_dir* to *dest_dir/source_dir*. If *dest_dir* does not exist, *rcp* creates it and copies the subtree rooted at *source_dir* to *dest_dir*.

### Constructing File and Directory Names

As indicated above, file and directory names contain one, two, or four component parts:

- **user_name**: Login name to be used for accessing directories and files on remote system.
- **hostname**: Hostname of remote system where directories and files are located.
- **pathname**: Absolute directory path name or directory path name relative to the login directory of user *user_name*.
- **filename**: Actual name of source or destination file. File name expansion is allowed on source file names.
- **dirname**: Actual name of source or destination directory subtree. File name expansion is allowed on source directory names.

Each file or directory argument is either a remote file name of the form *hostname:path*, or a local file name (with a slash (/) before any colon (:)). Hostname can be either an official host name or an alias (see hosts(4)). If hostname is of the form *ruser@host*, *ruser* is used on the remote host instead of the current user name. An unspecified path (that is, *hostname:*) refers to the remote user's login directory. If path does not begin with /, it is interpreted relative to the remote user's login directory on *hostname*. Shell metacharacters in remote paths can be quoted with backslash (\), single quotes (''), or double quotes (""), so that they will be interpreted remotely.

The rcp routine does not prompt for passwords. The current local user name or any user name specified via *ruser* must exist on *rhost* and allow remote command execution via remsh(1) and rcmd(3). remshd(1M) must be executable on the remote host.

Third-party transfers in the form:

```bash
rcp ruser1@rhost1:path1 ruser2@rhost2:path2
```

are performed as:

```bash
remsh rhost1 -l ruser1 rcp path1 ruser2@rhost2:path2
```

Therefore, for such a transfer to succeed, *ruser2* on *rhost2* must allow access by *ruser1* from *rhost1* (see hosts.equiv(4)).

## WARNINGS

The rcp routine is confused by any output generated by commands in a .cshrc file on the remote host (see csh(1)).

Copying a file onto itself, for example:

```bash
rcp path 'hostname:path'
```

may produce inconsistent results. The current HP-UX version of rcp simply copies the file over itself. However, some implementations of rcp, including some earlier HP-UX implementations, corrupt the file. In addition, the same file may be referred to in multiple ways, for example, via hard links, symbolic links, or NFS. It is not guaranteed that rcp will correctly copy a file over itself in all cases.

Implementations of rcp based on the 4.2BSD version (including the implementations of rcp prior to HP-UX 7.0) require that remote users be specified as *rhost.ruser*. If the first remote host specified in a third party transfer (*rhost1* in the example below) uses this older syntax, the command must have the form:

```bash
rcp ruser1@rhost1:path1 rhost2.ruser2:path2
```

since the target is interpreted by *rhost1*. A common problem that is encountered is when two remote files are to be copied to a remote target that specifies a remote user. If the two remote source systems, *rhost1* and *rhost2*, each expect a different form for the remote target, the command:

```bash
rcp rhost1:path1 rhost2:path2 rhost3.ruser3:path3
```

will certainly fail on one of the source systems. Perform such a transfer using two separate commands.

## AUTHOR

rcp was developed by the University of California, Berkeley.

## SEE ALSO

cp(1), ftp(1), remsh(1), remsh(1M), rcmd(3), hosts(4), hosts.equiv(4).

ftp Chapter in Using Internet Services.

# rcp(1) Secure Internet Services with Kerberos Authentication

## NAME

rcp - remote file copy

## SYNOPSIS

- Copy Single File:
  `rcp [-k realm] [-P] [-p] source_file1 dest_file`
- Copy Multiple Files:
  `rcp [-k realm] [-P] [-p] source_file1 [source_file2]... dest_dir`
- Copy One or More Directory Subtrees:
  `rcp [-k realm] [-P] [-p] -r source_dir1 [source_dir2]... dest_dir`
- Copy Files and Directory Subtrees:
  `rcp [-k realm] [-P] [-p] -r file_or_dir1 [file_or_dir2]... dest_dir`

## DESCRIPTION

The rcp command copies files, directory subtrees, or a combination of files and directory subtrees from one or more systems to another. In many respects, it is similar to the cp command (see cp(1)).

To use rcp, you must have read access to files being copied, and read and search (execute) permission on all directories in the directory path.

In a Kerberos V5 Network Authentication environment, rcp uses the Kerberos V5 protocol while initiating the connection to a remote host. The authorization mechanism is dependent on the command line options used to invoke remsh on the remote host (i.e., -K, -R, -r, or -k). Kerberos authentication and authorization rules are described in the Secure Internet Services man page, sis(5).

Although Kerberos authentication and authorization may apply, the Kerberos mechanism is not applied when copying files. The files are still transferred in cleartext over the network.

### Options and Arguments

rcp recognizes the following options and arguments:

- **source_file**: The name of an existing file or directory on a local or remote machine that you want copied to the specified destination. Source file and directory names are constructed as follows:
  `user_name@hostname:pathname/filename`
  or
  `user_name@hostname:pathname/dirname`
