
## PACKFILE OPTIMIZATION

When packing a blob fast-import always attempts to deltify against the last blob written. Unless specifically arranged for by the frontend, this will probably not be a prior version of the same file, so the generated delta will not be the smallest possible. The resulting packfile will be compressed, but will not be optimal.

Frontends which have efficient access to all revisions of a single file (for example reading an RCS/CVS ,v file) can choose to supply all revisions of that file as a sequence of consecutive blob commands. This allows fast-import to deltify the different file revisions against each other, saving space in the final packfile. Marks can be used to later identify individual file revisions during a sequence of commit commands.

The packfile(s) created by fast-import do not encourage good disk access patterns. This is caused by fast-import writing the data in the order it is received on standard input, while Git typically organizes data within packfiles to make the most recent (current tip) data appear before historical data. Git also clusters commits together, speeding up revision traversal through better cache locality.

For this reason it is strongly recommended that users repack the repository with `git repack -a -d` after fast-import completes, allowing Git to reorganize the packfiles for faster data access. If blob deltas are suboptimal (see above) then also adding the -f option to force recomputation of all deltas can significantly reduce the final packfile size (30-50% smaller can be quite typical).

## MEMORY UTILIZATION

There are a number of factors which affect how much memory fast-import requires to perform an import. Like critical sections of core Git, fast-import uses its own memory allocators to amortize any overheads associated with malloc. In practice fast-import tends to amortize any malloc overheads to 0, due to its use of large block allocations.

### per object

fast-import maintains an in-memory structure for every object written in this execution. On a 32 bit system the structure is 32 bytes, on a 64 bit system the structure is 40 bytes (due to the larger pointer sizes). Objects in the table are not deallocated until fast-import terminates. Importing 2 million objects on a 32 bit system will require approximately 64 MiB of memory.

The object table is actually a hashtable keyed on the object name (the unique SHA-1). This storage configuration allows fast-import to reuse an existing or already written object and avoid writing duplicates to the output packfile. Duplicate blobs are surprisingly common in an import, typically due to branch merges in the source.

### per mark

Marks are stored in a sparse array, using 1 pointer (4 bytes or 8 bytes, depending on pointer size) per mark. Although the array is sparse, frontends are still strongly encouraged to use marks between 1 and n, where n is the total number of marks required for this import.

### per branch

Branches are classified as active and inactive. The memory usage of the two classes is significantly different.

Inactive branches are stored in a structure which uses 96 or 120 bytes (32 bit or 64 bit systems, respectively), plus the length of the branch name (typically under 200 bytes), per branch. fast-import will easily handle as many as 10,000 inactive branches in under 2 MiB of memory.

Active branches have the same overhead as inactive branches, but also contain copies of every tree that has been recently modified on that branch. If subtree include has not been modified since the branch became active, its contents will not be loaded into memory, but if subtree src has been modified by a commit since the branch became active, then its contents will be loaded in memory.

As active branches store metadata about the files contained on that branch, their in-memory storage size can grow to a considerable size (see below). fast-import automatically moves active branches to inactive status based on a simple least-recently-used algorithm. The LRU chain is updated on each commit command. The maximum number of active branches can be increased or decreased on the command line with `--active-branches=`.

### per active tree

Trees (aka directories) use just 12 bytes of memory on top of the memory required for their entries (see “per active file” below). The cost of a tree is virtually 0, as its overhead amortizes out over the individual file entries.

### per active file entry

Files (and pointers to subtrees) within active trees require 52 or 64 bytes (32/64 bit platforms) per entry. To conserve space, file and tree names are pooled in a common string table, allowing the filename “Makefile” to use just 16 bytes (after including the string header overhead) no matter how many times it occurs within the project.

The active branch LRU, when coupled with the filename string pool and lazy loading of subtrees, allows fast-import to efficiently import projects with 2,000+ branches and 45,114+ files in a very limited memory footprint (less than 2.7 MiB per active branch).

## SIGNALS

Sending `SIGUSR1` to the *git fast-import* process ends the current packfile early, simulating a checkpoint command. The impatient operator can use this facility to peek at the objects and refs from an import in progress, at the cost of some added running time and worse compression.

## SEE ALSO

- (1)

## GIT-FETCH-PACK

### NAME

git-fetch-pack - Receive missing objects from another repository

### SYNOPSIS

```
git fetch-pack [-all] [--quiet|-q] [--keep|-k] [--thin] [--include-tag] [--upload-pack=<git-upload-pack>] [--depth=<n>] [--no-progress] [-v] <repository> [<refs>...]
```

### DESCRIPTION

Usually you would want to use *git fetch*, which is a higher level wrapper of this command, instead.

Invokes *git-upload-pack* on a possibly remote repository and asks it to send objects missing from this repository, to update the named heads. The list of commits available locally is found out by scanning the local refs/ hierarchy and sent to *git-upload-pack* running on the other end.

This command degenerates to download everything to complete the asked refs from the remote side when the local side does not have a common ancestor commit.

### OPTIONS

- `--all`
  Fetch all remote refs.

- `--stdin`
  Take the list of refs from stdin, one per line. If there are refs specified on the command line in addition to this option, then the refs from stdin are processed after those on the command line.
  
  If `--stateless-rpc` is specified together with this option then the list of refs must be in packet format (pkt-line). Each ref must be in a separate packet, and the list must end with a flush packet.

- `-q, --quiet`
  Pass `-q` flag to *git unpack-objects*; this makes the cloning process less verbose.

- `-k, --keep`
  Do not invoke *git unpack-objects* on received data, but create a single packfile out of it instead, and store it in the object database. If provided twice then the pack is locked against repacking.

- `--thin`
  Fetch a “thin” pack, which records objects in deltafied form based on objects not included in the pack to reduce network traffic.

- `--include-tag`
  If the remote side supports it, annotated tags objects will be downloaded on the same connection as the other objects if the object the tag references is downloaded. The caller must otherwise determine the tags this option made available.

- `--upload-pack=<git-upload-pack>`
  Use this to specify the path to *git-upload-pack* on the remote side, if is not found on your $PATH. Installations of sshd ignores the user’s environment setup scripts for login shells (e.g. *.bash_profile*) and your privately installed git may not be found on the system default $PATH. Another workaround suggested is to set up your $PATH in “*.bashrc*”, but this flag is for people who do not want to pay the overhead for non-interactive shells by having a lean *.bashrc* file (they set most of the things up in *.bash_profile*).

- `--exec=<git-upload-pack>`
  Same as `--upload-pack=<git-upload-pack>`.

- `--depth=<n>`
  Limit fetching to ancestor-chains not longer than n. *git-upload-pack* treats the special
