16.1  System Calls

603

# 16.1.3 Finding Directories and Files

The `File::Find` module lets you traverse a file system tree for specified files or directories based on some criteria, like the UNIX `find` command or the Perl `find2perl` translator.

# FORMAT

```
use File::Find;
find( \&wanted, '/dir1', '/dir2' );
sub wanted { ... }
```

The first argument to find() is either a hash reference describing the operations to be performed for each file or a reference to a subroutine. `Type perloc File::Find` for details. The wanted() function does whatever verification you want for the file. `File::Find::dir` contains the current directory name, and $_ is assigned the current filename within that directory. `File::Find::name` contains the complete pathname to the file. You are `chdir()`ed to `File::Find::dir` when the function is called, unless `no_chdir` was specified. The first argument to find() is either a hash reference describing the operations to be performed for each file or a code reference. See Table 16.5.

| **Table 16.5** Hash Reference Keys for File::Find |
| --- | --- |
| **Key** | **Value** |
| bydepth | Reports directory name after all entries have been reported. |
| follow | Follows symbolic links. |
| follow_fast | Similar to follow but may report files more than once. |
| follow_skip | Processes files (but not directories and symbolic links) only once. |
| no_chdir | Doesn't chdir to each directory as it recurses. |
| untaint | If -T (taint mode) is turned on, won't cd to directories that are tainted. |
| untaint_pattern | This should be set using the qr quoting operator. The default is set to `qr(^(/.+@\w/)+$)`. |
| untaint_skip | If set, directories (subtrees) that fail the untaint_pattern are skipped. The default is to `die` in such a case. |
| wanted | Used to specify the wanted function. |