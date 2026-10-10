
*CRAM-MD5*. If this is not set then *git imap-send* uses the basic IMAP plaintext LOGIN command.

## Examples

Using tunnel mode:

```ini
[imap] folder = "INBOX.Drafts" tunnel = "ssh -q -C /usr/bin/imapd ./Maildir 2>/dev/null"
```

Using direct mode:

```ini
[imap] folder = "INBOX.Drafts" host = user = bob pass = p455w0rd
```

Using direct mode with SSL:

```ini
[imap] folder = "INBOX.Drafts" host = user = bob pass = p455w0rd port = 123 sslverify = false
```

## EXAMPLE

To submit patches using GMail's IMAP interface, first, edit your ~/.gitconfig to specify your account settings:

```ini
[imap] folder = "[Gmail]/Drafts" host = user = port = 993 sslverify = false
```

You might need to instead use: `folder = "[Google Mail]/Drafts"` if you get an error that the “Folder doesn’t exist”.

Once the commits are ready to be sent, run the following command:

```bash
$ git format-patch --cover-letter -M --stdout origin/master | git imap-send
```

Just make sure to disable line wrapping in the email client (GMail's web interface will wrap lines no matter what, so you need to use a real IMAP client).

## CAUTION

It is still your responsibility to make sure that the email message sent by your email program meets the standards of your project. Many projects do not like patches to be attached. Some mail agents will transform patches (e.g. wrap lines, send them as format=flowed) in ways that make them fail. You will get angry flames ridiculing you if you don’t check this.

Thunderbird in particular is known to be problematic. Thunderbird users may wish to visit this web page for more information: m[]

## SEE ALSO

(1), (1), (5)

## GIT-INDEX-PACK

### NAME

git-index-pack - Build pack index file for an existing packed archive

### SYNOPSIS

```bash
git index-pack [-v] [-o <index-file>] <pack-file>
git index-pack --stdin [--fix-thin] [--keep] [-v] [-o <index-file>] [<pack-file>]
```

### DESCRIPTION

Reads a packed archive (.pack) from the specified file, and builds a pack index file (.idx) for it. The packed archive together with the pack index can then be placed in the objects/pack/ directory of a Git repository.

### OPTIONS

-   **-v**
    Be verbose about what is going on, including progress status.
-   **-o <index-file>**
    Write the generated pack index into the specified file. Without this option the name of pack index file is constructed from the name of packed archive file by replacing .pack with .idx (and the program fails if the name of packed archive does not end with .pack).
-   **--stdin**
    When this flag is provided, the pack is read from stdin instead and a copy is then written to `<pack-file>`. If `<pack-file>` is not specified, the pack is written to objects/pack/ directory of the current Git repository with a default name determined from the pack content. If `<pack-file>` is not specified consider using `--keep` to prevent a race condition between this process and git repack.
-   **--fix-thin**
    Fix a “thin” pack produced by `git pack-objects --thin` (see (1) for details) by adding the excluded objects the deltified objects are based on to the pack. This option only makes sense in conjunction with `--stdin`.
-   **--keep**
    Before moving the index into its final destination create an empty .keep file for the associated pack file. This option is usually necessary with `--stdin` to prevent a simultaneous git repack process from deleting the newly constructed pack and index before refs can be updated to use objects contained in the pack.
-   **--keep=<msg>**
    Like `--keep` create a .keep file before moving the index into its final destination, but rather than creating an empty file place `<msg>` followed by an LF into the .keep file. The `<msg>` message can later be searched for within all .keep files to locate any which have outlived their usefulness.
-   **--index-version=<version>[,<offset>]**
    This is intended to be used by the test suite only. It allows to force the version for the generated pack index, and to force 64-bit index entries on objects located above the given offset.
-   **--strict**
    Die, if the pack contains broken objects or links.
-   **--check-self-contained-and-connected**
    Die if the pack contains broken links. For internal use only.
-   **--threads=<n>**
    Specifies the number of threads to spawn when resolving deltas. This requires that index-pack be compiled with pthreads otherwise this option is ignored with a warning. This is meant to reduce packing time on multiprocessor machines. The required amount of memory for the delta search window is however multiplied by the number of threads. Specifying 0 will cause Git to auto-detect the number of CPU's and use maximum 3 threads.

## NOTE

Once the index has been created, the list of object names is sorted and the SHA-1 hash of that list is printed to stdout. If `--stdin` was also used then this is prefixed by either “pack\t”, or “keep\t” if a new .keep file was successfully created. This is useful to remove a .keep file used as a lock to prevent the race with *git repack* mentioned above.

## GIT-INIT-DB

### NAME

git-init-db - Creates an empty Git repository

### SYNOPSIS

```bash
git init-db [-q | --quiet] [-bare] [--template=<template_directory>]
[--separate-git-dir <git dir>] [--shared[=<permissions>]]
```

### DESCRIPTION

This is a synonym for (1). Please refer to the documentation of that command.

## GIT-INIT

### NAME

git-init - Create an empty Git repository or reinitialize an existing one

### SYNOPSIS

```bash
git init [-q | --quiet] [--bare] [--template=<template_directory>]
[--separate-git-dir <git dir>] [--shared[=<permissions>]] [directory]
```

### DESCRIPTION

This command creates an empty Git repository - basically a .git directory with subdirectories for objects, refs/heads, refs/tags, and template files. An initial HEAD file that references the HEAD of the master branch is also created.

If the $GIT_DIR environment variable is set then it specifies a path to use instead of ./.git for the base of the repository.

If the object storage directory is specified via the $GIT_OBJECT_DIRECTORY environment variable then the sha1 directories are created underneath - otherwise the default $GIT_DIR/objects directory is used.

Running *git init* in an existing repository is safe. It will not overwrite things that are already there. The primary reason for rerunning *git init* is to pick up newly added templates (or to move the repository to another place if `--separate-git-dir` is given).

### OPTIONS

-   **-q, --quiet**
    Only print error and warning messages; all other output will be suppressed.
-   **--bare**
    Create a bare repository. If GIT_DIR environment is not set, it is set to the current working directory.
-   **--template=<template_directory>**
    Specify the directory from which templates will be used. (See the “TEMPLATE DIRECTORY” section below.)
-   **--separate-git-dir=<git dir>**
    Instead of initializing the repository as a directory to either $GIT_DIR or ./.git/, create a text file there containing the path to the actual repository. This file acts as filesystem-agnostic Git symbolic link to the repository.
    
    If this is reinitialization, the repository will be moved to the specified path.
-   **--shared[=(false|true|umask|group|all|world|everybody|0xxx)]**
    Specify that the Git repository is to be shared amongst several users. This allows users belonging to the same group to push into that repository. When specified, the config variable “core.sharedRepository” is set so that files and directories under $GIT_DIR are created with the requested permissions. When not specified, Git will use permissions reported by (2).
    
    The option can have the following values, defaulting to group if no value is given:
    -   **umask (or false)**
        Use permissions reported by (2). The default, when --shared is not specified.
    -   **group (or true)**
        Make the repository group-writable, (and g+s, since the git group may not be the primary group of all users). This is used to loosen the permissions of an otherwise safe (2) value. Note that the umask still applies to the other permission bits (e.g. if umask is 0022, using group will not remove read privileges from other (non-group) users). See 0xxx for how to exactly specify the repository permissions.
    -   **all (or world or everybody)**
        Same as group, but make the repository readable by all users.
    -   **0xxx**
        0xxx is an octal number and each file will have mode 0xxx. 0xxx will override users’ (2) value (and not only loosen permissions as group and all does). 0640 will create a
